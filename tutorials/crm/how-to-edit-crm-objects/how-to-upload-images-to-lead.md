# Add Images to Lead Fields

> Scope: [`crm`](../../../api-reference/scopes/permissions.md)
>
> Who can execute the method: users with administrative access to the CRM section

Example of embedding a form on a website page that allows file attachments. After filling out the form, a new lead will be created in Bitrix24. The code below includes custom fields:

1. **UF_CRM_1551350435588** — multiple file property
2. **UF_CRM_1551362436225** — file property

- Create a form on the desired page:

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script>
    $(document).ready(function() {
        $('#form_to_crm_file').on('submit', function(el) {//event submit form
            el.preventDefault();//the default action of the event will not be triggered
            var formData = new FormData(this);
            var xhr = new XMLHttpRequest();
            xhr.open("POST", 'form.php'); // file for saving filled forms
            xhr.onreadystatechange = function () {
                if (this.readyState === 4) {
                    if (this.status >= 200 && this.status < 400) {
                        // Success!
                        var resp = this.responseText;
                        try {
                            var json = JSON.parse(resp);
                            if (typeof json.message !== 'undefined') {
                                alert(json.message);
                            }

                        } catch (e) {
                            return false;
                        }

                    } else {
                        alert('error');
                    }
                }
            };
            xhr.send(formData);
        });
    });
</script>
<form id="form_to_crm_file" method="post" enctype="multipart/form-data">
    <input type="text" name="NAME" placeholder="Name" required>
    <input type="text" name="LAST_NAME" placeholder="Last name">
    <input type="text" name="PHONE" placeholder="Phone">
    <input type="text" name="EMAIL" placeholder="E-mail">
    <input type="file" name="FILE" placeholder="File">
    <input type="file" name="FILES[]" placeholder="Files" multiple="multiple">

    <input type="submit" value="Submit">
</form>
```

- Create a file to save the filled forms:

{% list tabs %}

- JS

    ```js
    let sName = BX24.htmlspecialchars(BX24.getPost("NAME"));
    let sLastName = BX24.htmlspecialchars(BX24.getPost("LAST_NAME"));
    let sPhone = BX24.htmlspecialchars(BX24.getPost("PHONE"));
    let sEmail = BX24.htmlspecialchars(BX24.getPost("EMAIL"));
    // UF_CRM_1551350435588 - multiple file field
    // UF_CRM_1551362436225 - file field
    let arFiles = [];
    let arFile = [];

    // make array multiple files for add to custom field
    if (BX24.getFiles('FILES') && Array.isArray(BX24.getFiles('FILES').tmp_name)) {
        BX24.getFiles('FILES').tmp_name.forEach((path, k) => {
            arFiles.push({
                "fileData": [
                    BX24.getFiles('FILES').name[k],
                    base64Encode(fileGetContents(path))
                ]
            });
        });
    }

    // make file array for add to custom field
    if (BX24.getFiles('FILE') && BX24.getFiles('FILE').tmp_name) {
        arFile = {
            "fileData": [
                BX24.getFiles('FILE').name,
                base64Encode(fileGetContents(BX24.getFiles('FILE').tmp_name))
            ]
        };
    }

    // Format Phone and Email for saving
    let arPhone = sPhone ? [{ 'VALUE': sPhone, 'VALUE_TYPE': 'WORK' }] : [];
    let arEmail = sEmail ? [{ 'VALUE': sEmail, 'VALUE_TYPE': 'HOME' }] : [];

    BX24.callMethod(
        'crm.lead.add',
        {
            'fields': {
                'TITLE': 'From the site: ' + [sName, sLastName].join(' '), // *Lead Name[string]
                'NAME': sName, // Name[string]
                'UF_CRM_1551350435588': arFiles,
                'UF_CRM_1551362436225': arFile,
                'LAST_NAME': sLastName, // Last name[string]
                'PHONE': arPhone, // Phone[string]
                'EMAIL': arEmail // E-mail[string]
            }
        },
        function(result) {
            if (result.error()) {
                console.error(result.error());
                BX24.jsonEncode({ 'message': 'Lead not added: ' + result.error_description });
            } else {
                console.dir(result.data());
                BX24.jsonEncode({ 'message': 'Lead added' });
            }
        }
    );

    function fileGetContents(filePath) {
        // Implement file get contents
    }

    function base64Encode(data) {
        // Implement base64 encoding
    }
    ```

- PHP

    {% note info %}

    To use the examples in PHP, configure the *CRest* class and include the **crest.php** file in the files where this class is used. [More details](../../../how-to-use-examples.md)

    {% endnote %}

    ```php
    <?php
        $sName = htmlspecialchars($_POST["NAME"]);    
        $sLastName = htmlspecialchars($_POST["LAST_NAME"]);
        $sPhone = htmlspecialchars($_POST["PHONE"]);
        $sEmail = htmlspecialchars($_POST["EMAIL"]);
        //UF_CRM_1551350435588 - multiple file field
        //UF_CRM_1551362436225 - file field
        $arFiles = [];
        $arFile = [];
        //make array multiple files for add to custom field
        if(!empty($_FILES['FILES']['tmp_name']) && is_array($_FILES['FILES']['tmp_name'])){
            foreach($_FILES['FILES']['tmp_name'] as $k=>$path){
                $arFiles[] = [
                    "fileData" => [
                        $_FILES['FILES']['name'][$k],
                        base64_encode(file_get_contents($path))
                    ]
                ];
            }
        }
        //make file array for add to custom field
        if(!empty($_FILES['FILE']['tmp_name'])){
            $arFile = [
                "fileData" => [
                    $_FILES['FILE']['name'],
                    base64_encode(file_get_contents($_FILES['FILE']['tmp_name']))
                ]
            ];
        }
        //Format Phone and Email for saving
        $arPhone = (!empty($sPhone)) ? array(array('VALUE' => $sPhone, 'VALUE_TYPE' => 'WORK')) : array();
        $arEmail = (!empty($sEmail)) ? array(array('VALUE' => $sEmail, 'VALUE_TYPE' => 'HOME')) : array();

        $result = CRest::call(
            'crm.lead.add',
            [
            'fields' =>[
                'TITLE' => 'From the site: '.implode(' ',[$sName,$sLastName]),//*Lead Name[string]
                'NAME' => $sName,//Name[string]
                'UF_CRM_1551350435588' => $arFiles,
                'UF_CRM_1551362436225' => $arFile,
                'LAST_NAME' => $sLastName,//Last name[string]
                'PHONE' => $arPhone,//Phone[string]
                'EMAIL' => $arEmail,//E-mail[string]
            ]
        ]);
        if(!empty($result['result'])){
            echo json_encode(['message' => 'Lead added']);
        }elseif(!empty($result['error_description'])){
            echo json_encode(['message' => 'Lead not added: '.$result['error_description']]);
        }else{
            echo json_encode(['message' => 'Lead not added']);
        }
    ?>
    ```

{% endlist %}