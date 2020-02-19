# Baja
Deberás de usar el REST endpoint correspondiente dependiendo del servidor que utilizas: XML Builder o XML Builder Signer.

## XML Builder endpoints
| METHOD    | ENDPOINT                              |
| --------- | --------------------------------------|
| POST      | /api/documents/voided-document/create |

## XML Builder Signer endpoint

| METHOD    | ENDPOINT                                                              |
| --------- | ----------------------------------------------------------------------|
| POST      | /api/organizations/{organizationId}/documents/voided-document/create  |

## Ejemplo
El siguiente JSON puede ser usado para crear una Baja:

```json
{
  "numero": 1,
  "proveedor": {
    "ruc": "12345678912",
    "razonSocial": "Project OpenUBL",
    "codigoPostal": "050101"
  },
  "tipoDocumentReference": "FACTURA",
  "fechaEmisionDocumentReference": 1582066800000,
  "serieNumeroDocumentReference": "F001-1",
  "motivoBajaDocumentReference": "El motivo de baja del comprobante"
}
```

XML resultado:

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<VoidedDocuments xmlns="urn:sunat:names:specification:ubl:peru:schema:xsd:VoidedDocuments-1"
                 xmlns:cac="urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2"
                 xmlns:cbc="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2"
                 xmlns:ds="http://www.w3.org/2000/09/xmldsig#"
                 xmlns:ext="urn:oasis:names:specification:ubl:schema:xsd:CommonExtensionComponents-2"
                 xmlns:sac="urn:sunat:names:specification:ubl:peru:schema:xsd:SunatAggregateComponents-1"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <ext:UBLExtensions>
        <ext:UBLExtension>
            <ext:ExtensionContent />
        </ext:UBLExtension>
    </ext:UBLExtensions>
    <cbc:UBLVersionID>2.0</cbc:UBLVersionID>
    <cbc:CustomizationID>1.0</cbc:CustomizationID>
    <cbc:ID>RA-20200219-1</cbc:ID>
    <cbc:ReferenceDate>2020-02-18</cbc:ReferenceDate>
    <cbc:IssueDate>2020-02-19</cbc:IssueDate>
    <cac:Signature>
        <cbc:ID>#SIGN-ID</cbc:ID>
        <cac:SignatoryParty>
            <cac:PartyIdentification>
                <cbc:ID>12345678912</cbc:ID>
            </cac:PartyIdentification>
            <cac:PartyName>
                <cbc:Name><![CDATA[Project OpenUBL]]></cbc:Name>
            </cac:PartyName>
        </cac:SignatoryParty>
        <cac:DigitalSignatureAttachment>
            <cac:ExternalReference>
                <cbc:URI>#SIGN-ID</cbc:URI>
            </cac:ExternalReference>
        </cac:DigitalSignatureAttachment>
    </cac:Signature>
    <cac:AccountingSupplierParty>
        <cbc:CustomerAssignedAccountID>12345678912</cbc:CustomerAssignedAccountID>
        <cbc:AdditionalAccountID>6</cbc:AdditionalAccountID>
        <cac:Party>
                <cac:PostalAddress>
                    <cbc:ID>050101</cbc:ID>
                </cac:PostalAddress>
            <cac:PartyLegalEntity>
                <cbc:RegistrationName>Project OpenUBL</cbc:RegistrationName>
            </cac:PartyLegalEntity>
        </cac:Party>
    </cac:AccountingSupplierParty>
    <sac:VoidedDocumentsLine>
        <cbc:LineID>1</cbc:LineID>
        <cbc:DocumentTypeCode>01</cbc:DocumentTypeCode>
        <sac:DocumentSerialID>F001</sac:DocumentSerialID>
        <sac:DocumentNumberID>1</sac:DocumentNumberID>
        <sac:VoidReasonDescription>El motivo de baja del comprobante</sac:VoidReasonDescription>
    </sac:VoidedDocumentsLine>
</VoidedDocuments>
```
