# How to Add a Deal and Company with Requisites

> Scope: [`crm`](../../../api-reference/scopes/permissions.md)
>
> Who can execute the method: users with administrative access to the CRM section

An example of embedding a form on a website page, after filling out which a new deal is created in Bitrix24, along with a new company that has requisites attached.

- Create a form on the desired page:

{% list tabs %}

- JS

    ```javascript
    BX24.callMethod(
        'crm.address.fields',
        {},
        function(arAddressFields) {
            BX24.callMethod(
                'crm.requisite.preset.list',
                {
                    'select': ["ID", "NAME"]
                },
                function(arRequisiteType) {
                    if (arRequisiteType.error()) {
                        console.error(arRequisiteType.error());
                        return;
                    }

                    arRequisiteType = arRequisiteType.data().reduce((acc, item) => {
                        acc[item.ID] = item.NAME;
                        return acc;
                    }, {});

                    delete arAddressFields.result.TYPE_ID;
                    delete arAddressFields.result.ENTITY_TYPE_ID;
                    delete arAddressFields.result.ENTITY_ID;
                    delete arAddressFields.result.COUNTRY_CODE;
                    delete arAddressFields.result.ANCHOR_TYPE_ID;
                    delete arAddressFields.result.ANCHOR_ID;

                    let formHtml = '<form id="form_to_crm">';
                    formHtml += '<select name="REQ_TYPE" required>';
                    formHtml += '<option value="" disabled selected>Select</option>';
                    for (let id in arRequisiteType) {
                        formHtml += `<option value="${id}">${arRequisiteType[id]}</option>`;
                    }
                    formHtml += '</select>';
                    formHtml += '<input type="text" name="TITLE" placeholder="Org name" required>';
                    formHtml += '<input type="text" name="INN" placeholder="INN">';
                    formHtml += '<input type="text" name="PHONE" placeholder="Phone">';

                    if (Array.isArray(arAddressFields.result)) {
                        for (let key in arAddressFields.result) {
                            let arField = arAddressFields.result[key];
                            formHtml += `<input type="text" name="ADDRESS[${key}]" placeholder="${arField.title}" ${arField.isRequired ? 'required' : ''}>`;
                        }
                    }

                    formHtml += '<input type="submit" value="Submit">';
                    formHtml += '</form>';

                    document.body.innerHTML = formHtml;

                    document.getElementById('form_to_crm').addEventListener('submit', function(el) {
                        el.preventDefault();
                        let formData = new FormData(this);
                        fetch('form.php', {
                            method: 'POST',
                            body: formData
                        })
                        .then(response => response.json())
                        .then(data => {
                            alert(data.message);
                        })
                        .catch(error => {
                            console.error('Error:', error);
                        });
                    });
                }
            );
        }
    );
    ```

- PHP

    {% note info %}

    To use the PHP examples, configure the *CRest* class and include the **crest.php** file in the files where this class is used. [Learn more](../../../how-to-use-examples.md)

    {% endnote %}

    ```php
    <?php
    $arAddressFields = CRest::call('crm.address.fields',[]);
    /*
    crm.address.fields return: https://dev.quickbooks.com/rest_help/crm/requisite/requisite_fields.php#address
    */
    $arRequisiteType = CRest::call('crm.requisite.preset.list',
        [
            'select'=>[
                "ID", "NAME"
            ]
        ]
    );
    if(!empty($arRequisiteType['result'])):
        $arRequisiteType = array_column($arRequisiteType['result'],'NAME','ID');
        //unset system address fields
        unset($arAddressFields['result']['TYPE_ID']);
        unset($arAddressFields['result']['ENTITY_TYPE_ID']);
        unset($arAddressFields['result']['ENTITY_ID']);
        //unset uninteresting address fields
        unset($arAddressFields['result']['COUNTRY_CODE']);
        unset($arAddressFields['result']['ANCHOR_TYPE_ID']);
        unset($arAddressFields['result']['ANCHOR_ID']);
        ?>
        <form id="form_to_crm">
            <select name="REQ_TYPE" required>
                <option value="" disabled selected>Select</option>
                <?php foreach($arRequisiteType as $id=>$name):?>
                    <option value="<?=$id?>"><?=$name?></option>
                <?php endforeach;?>
            </select>
            <input type="text" name="TITLE" placeholder="Org name" required>
            <input type="text" name="INN" placeholder="INN">
            <input type="text" name="PHONE" placeholder="Phone">
            <?php if(is_array($arAddressFields['result'])):?>
                <?php foreach($arAddressFields['result'] as $key=>$arField):?>
                    <input type="text" name="ADDRESS[<?=$key?>]" placeholder="<?=$arField['title']?>" <?=($arField['isRequired'])?'required':'';?>>
                <?php endforeach;?>
            <?php endif;?>
            <input type="submit" value="Submit">
        </form>
    <?php else:?>
        No requisite types.
    <?php endif;?>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
    <script>
    $(document).ready(function() {
        $('#form_to_crm').on( 'submit', function(el) {//event submit form
            el.preventDefault();//the default action of the event will not be triggered
            var formData = $(this).serialize();
            $.ajax({
                'method': 'POST',
                'dataType': 'json',
                'url': 'form.php', // file for saving filled forms
                'data': formData,
                success: function(data){//success callback
                    alert(data.message);
                }
            });
        });
    });
    </script>
    ```

{% endlist %}



- Create a file to save the filled forms:

{% list tabs %}

- JS

    ```js
    document.addEventListener('DOMContentLoaded', function() {
        document.getElementById('form_to_crm').addEventListener('submit', function(el) {
            el.preventDefault();
            let formData = new FormData(this);
            let iRequisitePresetID = parseInt(formData.get("REQ_TYPE"));
            let sTitle = formData.get("TITLE");
            let sINN = formData.get("INN");
            let sPhone = formData.get("PHONE");
            let arAddress = {};

            formData.forEach((value, key) => {
                if (key.startsWith("ADDRESS[")) {
                    let addressKey = key.match(/ADDRESS\[(.*)\]/)[1];
                    arAddress[addressKey] = value;
                }
            });

            arAddress['TYPE_ID'] = 1;
            arAddress['ENTITY_TYPE_ID'] = 8;

            let arPhone = sPhone ? [{ 'VALUE': sPhone, 'VALUE_TYPE': 'WORK' }] : [];

            BX24.callMethod(
                'crm.company.add',
                {
                    'fields': {
                        'TITLE': sTitle,
                        'COMPANY_TYPE': 'CUSTOMER',
                        'PHONE': arPhone
                    }
                },
                function(result) {
                    if (result.error()) {
                        console.error(result.error());
                        alert('not added: ' + result.error_description());
                        return;
                    }

                    let companyId = result.data();
                    BX24.callMethod(
                        'crm.requisite.add',
                        {
                            'fields': {
                                'ENTITY_TYPE_ID': 4,
                                'ENTITY_ID': companyId,
                                'PRESET_ID': iRequisitePresetID,
                                'TITLE': sTitle,
                                'ACTIVE': 'Y',
                                'NAME': sTitle,
                                'RQ_INN': sINN
                            }
                        },
                        function(resultRequisite) {
                            if (resultRequisite.error()) {
                                console.error(resultRequisite.error());
                                alert('not added: ' + resultRequisite.error_description());
                                return;
                            }

                            let requisiteId = resultRequisite.data();
                            let arDealFields = {
                                'TITLE': sTitle,
                                'COMPANY_ID': companyId
                            };

                            if (requisiteId) {
                                arDealFields['REQUISITE_ID'] = requisiteId;
                                arAddress['ENTITY_ID'] = requisiteId;

                                BX24.callMethod(
                                    'crm.address.add',
                                    {
                                        'fields': arAddress
                                    },
                                    function(resultAddress) {
                                        if (resultAddress.error()) {
                                            console.error(resultAddress.error());
                                            alert('not added: ' + resultAddress.error_description());
                                            return;
                                        }
                                    }
                                );
                            }

                            BX24.callMethod(
                                'crm.deal.add',
                                {
                                    'fields': arDealFields
                                },
                                function(resultDeal) {
                                    if (resultDeal.error()) {
                                        console.error(resultDeal.error());
                                        alert('not added: ' + resultDeal.error_description());
                                        return;
                                    }

                                    alert('add');
                                }
                            );
                        }
                    );
                }
            );
        });
    });
    ```

- PHP

    {% note info %}

    To use the PHP examples, configure the *CRest* class and include the **crest.php** file in the files where this class is used. [Learn more](../../../how-to-use-examples.md)

    {% endnote %}

    ```php
    <?php
    $iRequisitePresetID = intVal($_POST["REQ_TYPE"]);
    $sTitle = htmlspecialchars($_POST["TITLE"]);
    $sINN = htmlspecialchars($_POST["INN"]);
    $sPhone = htmlspecialchars($_POST["PHONE"]);
    $arAddress = [];

    foreach($_POST["ADDRESS"] as $key=>$val){
        $arAddress[$key] = htmlspecialchars($val);
    }
    $arAddress['TYPE_ID'] = 1;//1 is actual address in CRest::call('crm.enum.addresstype');
    $arAddress['ENTITY_TYPE_ID'] = 8;//8 - is requisite in CRest::call('crm.enum.ownertype');

    $arPhone = (!empty($sPhone)) ? array(array('VALUE' => $sPhone, 'VALUE_TYPE' => 'WORK')) : array();

    $result = CRest::call(
        'crm.company.add',
        [
            'fields' =>[
                'TITLE' => $sTitle,
                'COMPANY_TYPE' => 'CUSTOMER',//is Client in CRest::call('crm.status.list',['filter'=>['ENTITY_ID'=>'COMPANY_TYPE']])
                'PHONE' => $arPhone,
            ]
        ]
    );
    if(!empty($result['result'])){
        $resultRequisite = CRest::call(
            'crm.requisite.add',
            [
                'fields' =>[
                    'ENTITY_TYPE_ID' => 4,//4 - is company in CRest::call('crm.enum.ownertype');
                    'ENTITY_ID' => $result['result'],//company id
                    'PRESET_ID' => $iRequisitePresetID,
                    'TITLE' => $sTitle,
                    'ACTIVE' => 'Y',
                    'NAME' => $sTitle,
                    'RQ_INN' => $sINN,
                ]
            ]
        );
        $arDealFields = [
            'TITLE' => $sTitle,
            'COMPANY_ID' => $result['result']
        ];
        if(!empty($resultRequisite['result'])){
            $arDealFields['REQUISITE_ID'] = $resultRequisite['result'];//add requisite to deal is analogue "crm.requisite.link.list"
            $arAddress['ENTITY_ID'] = $resultRequisite['result'];//id requisite
            $resultAddress = CRest::call(
                'crm.address.add',
                [
                    'fields' =>$arAddress
                ]
            );
        }
        $resultDeal = CRest::call(
            'crm.deal.add',
            [
                'fields' => $arDealFields
            ]
        );
        echo json_encode(['message' => 'add']);
    }elseif(!empty($result['error_description'])){
        echo json_encode(['message' => 'not added: '.$result['error_description']]);
    }else{
        echo json_encode(['message' => 'not added']);
    }
    ?>
    ```

{% endlist %}