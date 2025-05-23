# How to Change Product Custom Field Values

{% if build == 'dev' %}

{% note alert "TO-DO _not exported to prod_" %}

Removed from the menu to prevent publication. Needs a complete overhaul, crm.product.* is outdated.

{% endnote %}

{% endif %}

> Scope: [`crm`](../../../api-reference/scopes/permissions.md)
>
> Who can execute the method: users with administrative access to the CRM section

Examples of working with various product properties.

To run the examples, you need to create a folder **/pictures** next to the executable file of the example and fill it with images named "1.jpg" — "6.jpg". Also, at the beginning of the example, you need to update the variable values from the example to your own:

- `propertyIDSelect` — identifier of the single-select property
- `propertySelectValueID` — identifier of the value of the single-select property
- `propertyIDMultiSelect` — identifier of the multi-select property
- `propertyMultiSelectValueID` — identifiers of the values of the multi-select property
- `propertyIDFile` — identifier of the single file property
- `propertyIDMultiFile` — identifier of the multi-file property

## Changing a Product

{% list tabs %}

- JS

    ```js
    let idProduct = 10339;

    let propertyIDSelect = 106;
    let propertySelectValueID = 85;

    let propertyIDMultiSelect = 105;
    let propertyMultiSelectValueID = [79, 80, 82];

    let propertyIDFile = 107;
    let propertyFilePathToPicture = 'pictures/1.jpg'; // relative or full path on server

    let propertyIDMultiFile = 108;
    let propertyMultiFilePathToPicture = [ // relative or full path on server
        'pictures/2.jpg',
        'pictures/3.jpg',
        'pictures/4.jpg',
    ];

    let standardPreviewPicturePath = 'pictures/5.jpg'; // relative or full path on server
    let standardDetailPicturePath = 'pictures/6.jpg'; // relative or full path on server

    let arFields = {
        'NAME': 'Example product 2',
        'CURRENCY_ID': 'USD',
        'PRICE': 4900,
        'SORT': 500
    };

    BX24.callMethod(
        'crm.product.get',
        {
            'id': idProduct
        },
        function(result) {
            if (result.error()) {
                console.error(result.error());
            } else {
                let arProduct = result.data();
                if (propertyIDSelect > 0 && propertySelectValueID > 0) {
                    arFields['PROPERTY_' + propertyIDSelect] = propertySelectValueID;
                }

                if (propertyIDMultiSelect > 0 && Array.isArray(propertyMultiSelectValueID) && propertyMultiSelectValueID.length > 0) {
                    arFields['PROPERTY_' + propertyIDMultiSelect] = propertyMultiSelectValueID;
                }

                if (propertyIDFile > 0 && propertyFilePathToPicture && fileExists(propertyFilePathToPicture)) {
                    let fileName = propertyFilePathToPicture.split('/').pop();
                    arFields['PROPERTY_' + propertyIDFile] = {
                        "fileData": [
                            fileName,
                            base64Encode(fileGetContents(propertyFilePathToPicture))
                        ]
                    };
                }

                if (propertyIDMultiFile > 0 && Array.isArray(propertyMultiFilePathToPicture) && propertyMultiFilePathToPicture.length > 0) {
                    arFields['PROPERTY_' + propertyIDMultiFile] = [];
                    propertyMultiFilePathToPicture.forEach(function(path) {
                        if (fileExists(path)) {
                            let fileName = path.split('/').pop();
                            arFields['PROPERTY_' + propertyIDMultiFile].push({
                                "fileData": [
                                    fileName,
                                    base64Encode(fileGetContents(path))
                                ]
                            });
                        }
                    });
                }

                if (standardPreviewPicturePath && fileExists(standardPreviewPicturePath)) {
                    let fileName = standardPreviewPicturePath.split('/').pop();
                    arFields['PREVIEW_PICTURE'] = {
                        "fileData": [
                            fileName,
                            base64Encode(fileGetContents(standardPreviewPicturePath))
                        ]
                    };
                }

                if (standardDetailPicturePath && fileExists(standardDetailPicturePath)) {
                    let fileName = standardDetailPicturePath.split('/').pop();
                    arFields['DETAIL_PICTURE'] = {
                        "fileData": [
                            fileName,
                            base64Encode(fileGetContents(standardDetailPicturePath))
                        ]
                    };
                }
            }
        }
    );

    function fileExists(filePath) {
        // Implement file existence check
    }

    function fileGetContents(filePath) {
        // Implement file get contents
    }

    function base64Encode(data) {
        // Implement base64 encoding
    }

    // delete old files
    let arPropsFile = [
        'PREVIEW_PICTURE',
        'DETAIL_PICTURE',
    ];
    if (propertyIDFile > 0) {
        arPropsFile.push('PROPERTY_' + propertyIDFile);
    }
    if (propertyIDMultiFile > 0) {
        arPropsFile.push('PROPERTY_' + propertyIDMultiFile);
    }
    arPropsFile.forEach(function(prop) {
        if (!arFields[prop]) { // if property does not change file don't delete old file
            return;
        }

        if (arProduct[prop] && arProduct[prop].id) { // for standard fields PREVIEW_PICTURE and DETAIL_PICTURE
            arFields[prop].push({
                'id': arProduct[prop].id,
                'remove': 'Y'
            });
        } else if (arProduct[prop] && arProduct[prop].value && arProduct[prop].value.id) { // for property type file
            arFields[prop].push({
                'valueId': arProduct[prop].valueId,
                'value': {
                    'id': arProduct[prop].value.id,
                    'remove': 'Y'
                }
            });
        } else if (!arProduct[prop].value && Array.isArray(arProduct[prop])) { // for property type multiple file
            arProduct[prop].forEach(function(file) {
                if (file.value && file.value.id) {
                    arFields[prop].push({
                        'valueId': file.valueId,
                        'value': {
                            'id': file.value.id,
                            'remove': 'Y'
                        }
                    });
                }
            });
        }
    });

    BX24.callMethod(
        'crm.product.update',
        {
            'id': idProduct,
            'fields': arFields
        },
        function(result) {
            if (result.error()) {
                console.error(result.error());
            } else {
                console.dir(result.data());
            }
        }
    );
    ```

- PHP

    {% note info %}

    To use the examples in PHP, configure the *CRest* class and include the **crest.php** file in the files where this class is used. [More details](../../../how-to-use-examples.md)

    {% endnote %}

    ```php
    $idProduct = 10339;

    $propertyIDSelect = 106;
    $propertySelectValueID = 85;

    $propertyIDMultiSelect = 105;
    $propertyMultiSelectValueID = [79, 80, 82];

    $propertyIDFile = 107;
    $propertyFilePathToPicture = 'pictures/1.jpg'; // relative or full path on server

    $propertyIDMultiFile = 108;
    $propertyMultiFilePathToPicture = [ // relative or full path on server
        'pictures/2.jpg',
        'pictures/3.jpg',
        'pictures/4.jpg',
    ];

    $standardPreviewPicturePath = 'pictures/5.jpg'; // relative or full path on server
    $standardDetailPicturePath = 'pictures/6.jpg'; // relative or full path on server

    $arFields = [
        'NAME' => 'Example product 2',
        'CURRENCY_ID' => 'USD',
        'PRICE' => 4900,
        'SORT' => 500
    ];

    $result = CRest::call(
        'crm.product.get',
        [
            'id' => $idProduct
        ]
    );
    if (!empty($result['result']))
    {
        $arProduct = $result['result'];
        if ($propertyIDSelect > 0 && $propertySelectValueID > 0)
        {
            $arFields['PROPERTY_' . $propertyIDSelect] = $propertySelectValueID;
        }

        if ($propertyIDMultiSelect > 0 && is_array($propertyMultiSelectValueID) && count($propertyMultiSelectValueID) > 0)
        {
            $arFields['PROPERTY_' . $propertyIDMultiSelect] = $propertyMultiSelectValueID;
        }

        if ($propertyIDFile > 0 && !empty($propertyFilePathToPicture) && file_exists($propertyFilePathToPicture))
        {
            $fileName = end(explode('/', $propertyFilePathToPicture));
            $arFields['PROPERTY_' . $propertyIDFile] = [
                "fileData" => [
                    $fileName,
                    base64_encode(file_get_contents($propertyFilePathToPicture))
                ]
            ];
        }
        if ($propertyIDMultiFile > 0 &&
            is_array($propertyMultiFilePathToPicture) &&
            count($propertyMultiFilePathToPicture) > 0)
        {
            foreach ($propertyMultiFilePathToPicture as $path)
            {
                if (file_exists($path))
                {
                    $fileName = end(explode('/', $path));
                    $arFields['PROPERTY_' . $propertyIDMultiFile][] = [
                        "fileData" => [
                            $fileName,
                            base64_encode(file_get_contents($path))
                        ]
                    ];
                }
            }
        }
        if (!empty($standardPreviewPicturePath) && file_exists($standardPreviewPicturePath))
        {
            $fileName = end(explode('/', $standardPreviewPicturePath));
            $arFields['PREVIEW_PICTURE'] = [
                "fileData" => [
                    $fileName,
                    base64_encode(file_get_contents($standardPreviewPicturePath))
                ]
            ];
        }
        if (!empty($standardDetailPicturePath) && file_exists($standardDetailPicturePath))
        {
            $fileName = end(explode('/', $standardDetailPicturePath));
            $arFields['DETAIL_PICTURE'] = [
                "fileData" => [
                    $fileName,
                    base64_encode(file_get_contents($standardDetailPicturePath))
                ]
            ];
        }

        //delete old files
        $arPropsFile = [
            'PREVIEW_PICTURE',
            'DETAIL_PICTURE',
        ];
        if ($propertyIDFile > 0)
        {
            $arPropsFile[] = 'PROPERTY_' . $propertyIDFile;
        }
        if ($propertyIDMultiFile > 0)
        {
            $arPropsFile[] = 'PROPERTY_' . $propertyIDMultiFile;
        }
        foreach ($arPropsFile as $prop)
        {
            if (empty($arFields[$prop])) // if property does not change file don't delete old file
            {
                continue;
            }

            if (!empty($arProduct[$prop]['id'])) // for standard fields PREVIEW_PICTURE and DETAIL_PICTURE
            {
                $arFields[$prop][] = [
                    'id' => $arProduct[$prop]['id'],
                    'remove' => 'Y',
                ];
            }
            elseif (!empty($arProduct[$prop]['value']['id'])) // for property type file
            {
                $arFields[$prop][] = [
                    'valueId' => $arProduct[$prop]['valueId'],
                    'value' => [
                        'id' => $arProduct[$prop]['value']['id'],
                        'remove' => 'Y',
                    ]
                ];
            }
            elseif (!isset($arProduct[$prop]['value']) && is_array($arProduct[$prop])) // for property type multiple file
            {
                foreach ($arProduct[$prop] as $file)
                {
                    if (!empty($file['value']['id']))
                    {
                        $arFields[$prop][] = [
                            'valueId' => $file['valueId'],
                            'value' => [
                                'id' => $file['value']['id'],
                                'remove' => 'Y',
                            ]
                        ];
                    }

                }
            }
        }

        $result = CRest::call(
            'crm.product.update',
            [
                'id' => $idProduct,
                'fields' => $arFields
            ]
        );

    }
    ```

{% endlist %}

## Clearing Properties with Files in a Product

{% list tabs %}

- JS

    ```javascript
    let idProduct = 10339;

    let propertyIDFile = 107;
    let propertyIDMultiFile = 108;

    BX24.callMethod(
        'crm.product.get',
        {
            'id': idProduct
        },
        function(result) {
            if (result.error()) {
                console.error(result.error());
            } else {
                let arProduct = result.data();
                let arPropsFile = [
                    'PREVIEW_PICTURE',
                    'DETAIL_PICTURE',
                ];
                if (propertyIDFile > 0) {
                    arPropsFile.push('PROPERTY_' + propertyIDFile);
                }
                if (propertyIDMultiFile > 0) {
                    arPropsFile.push('PROPERTY_' + propertyIDMultiFile);
                }
                let arSaveData = {};
                arPropsFile.forEach(function(prop) {
                    if (arProduct[prop] && arProduct[prop].id) { // for standard fields PREVIEW_PICTURE and DETAIL_PICTURE
                        arSaveData[prop] = {
                            'id': arProduct[prop].id,
                            'remove': 'Y'
                        };
                    } else if (arProduct[prop] && arProduct[prop].value && arProduct[prop].value.id) { // for property type file
                        arSaveData[prop] = {
                            'valueId': arProduct[prop].valueId,
                            'value': {
                                'id': arProduct[prop].value.id,
                                'remove': 'Y'
                            }
                        };
                    } else if (!arProduct[prop].value && Array.isArray(arProduct[prop])) { // for property type multiple file
                        arProduct[prop].forEach(function(file) {
                            if (file.value && file.value.id) {
                                if (!arSaveData[prop]) {
                                    arSaveData[prop] = [];
                                }
                                arSaveData[prop].push({
                                    'valueId': file.valueId,
                                    'value': {
                                        'id': file.value.id,
                                        'remove': 'Y'
                                    }
                                });
                            }
                        });
                    }
                });

                BX24.callMethod(
                    'crm.product.update',
                    {
                        'id': idProduct,
                        'fields': arSaveData
                    },
                    function(resultSave) {
                        if (resultSave.error()) {
                            console.error(resultSave.error());
                        } else {
                            console.dir(resultSave.data());
                        }
                    }
                );
            }
        }
    );
    ```

- PHP

    {% note info %}

    To use the examples in PHP, configure the *CRest* class and include the **crest.php** file in the files where this class is used. [More details](../../../how-to-use-examples.md)

    {% endnote %}

    ```php
    $idProduct = 10339;

    $propertyIDFile = 107;
    $propertyIDMultiFile = 108;

    $result = CRest::call(
        'crm.product.get',
        [
            'id' => $idProduct
        ]
    );

    if (!empty($result['result']))
    {
        $arProduct = $result['result'];
        $arPropsFile = [
            'PREVIEW_PICTURE',
            'DETAIL_PICTURE',
        ];
        if ($propertyIDFile > 0)
        {
            $arPropsFile[] = 'PROPERTY_' . $propertyIDFile;
        }
        if ($propertyIDMultiFile > 0)
        {
            $arPropsFile[] = 'PROPERTY_' . $propertyIDMultiFile;
        }
        $arSaveData = [];
        foreach ($arPropsFile as $prop)
        {
            if (!empty($arProduct[$prop]['id'])) // for standard fields PREVIEW_PICTURE and DETAIL_PICTURE
            {
                $arSaveData[$prop] = [
                    'id' => $arProduct[$prop]['id'],
                    'remove' => 'Y',
                ];
            }
            elseif (!empty($arProduct[$prop]['value']['id'])) // for property type file
            {
                $arSaveData[$prop] = [
                    'valueId' => $arProduct[$prop]['valueId'],
                    'value' => [
                        'id' => $arProduct[$prop]['value']['id'],
                        'remove' => 'Y',
                    ]
                ];
            }
            elseif (!isset($arProduct[$prop]['value']) && is_array($arProduct[$prop])) // for property type multiple file
            {
                foreach ($arProduct[$prop] as $file)
                {
                    if (!empty($file['value']['id']))
                    {
                        $arSaveData[$prop][] = [
                            'valueId' => $file['valueId'],
                            'value' => [
                                'id' => $file['value']['id'],
                                'remove' => 'Y',
                            ]
                        ];
                    }

                }
            }
        }
    }

    $resultSave = CRest::call(
        'crm.product.update',
        [
            'id' => $idProduct,
            'fields' => $arSaveData
        ]
    );
    ```

{% endlist %}