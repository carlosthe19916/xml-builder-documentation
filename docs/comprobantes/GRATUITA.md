# Comprobantes gratuitos
Deberás de usar el REST endpoint correspondiente dependiendo del servidor que utilizas (XML Builder o XML Builder Signer) y dependiendo del comprobante que desees crear.

## XML Builder endpoints
| METHOD    | ENDPOINT                          |
| --------- | ----------------------------------|
| POST      | /api/documents/invoice/create     |
| POST      | /api/documents/credit-note/create     |
| POST      | /api/documents/debit-note/create     |

## XML Builder Signer endpoints

| METHOD    | ENDPOINT                                                          |
| --------- | ------------------------------------------------------------------|
| POST      | /api/organizations/{organizationId}/documents/invoice/create      |
| POST      | /api/organizations/{organizationId}/documents/credit-note/create  |
| POST      | /api/organizations/{organizationId}/documents/debit-note/create   |

## ¿Qué campo utilizar? 
Se debe de utilizar el campo `detalle.tipoIGV`:

```json
{
  "detalle": [
    {
      "tipoIGV": "GRAVADO_RETIRO_POR_PREMIO"
    }
  ]
}
```

Los posibles valores de `tipoIGV` para una operación gratuita son:

| Valor                                 | Código |
| ----------------------------------------- | --:|
| GRAVADO_RETIRO_POR_PREMIO                 | 11 |
| GRAVADO_RETIRO_POR_DONACION               | 12 |
| GRAVADO_RETIRO                            | 13 |
| GRAVADO_RETIRO_POR_PUBLICIDAD             | 14 |
| GRAVADO_BONIFICACIONES                    | 15 |
| GRAVADO_RETIRO_POR_ENTREGA_A_TRABAJADORES | 16 |
| GRAVADO_IVAP                              | 17 |
| EXONERADO_TRANSFERENCIA_GRATUITA          | 21 |
| INAFECTO_RETIRO_POR_BONIFICACION          | 31 |
| INAFECTO_RETIRO                           | 32 |
| INAFECTO_RETIRO_POR_MUESTRAS_MEDICAS      | 33 |
| INAFECTO_RETIRO_POR_CONVENIO_COLECTIVO    | 34 |
| INAFECTO_RETIRO_POR_PREMIO                | 35 |
| INAFECTO_RETIRO_POR_PUBLICIDAD            | 36 |


## Ejemplo
Factura gratuita:

```json
{
  "serie": "F001",
  "numero": 1,
  "proveedor": {
    "ruc": "12345678912",
    "razonSocial": "Project OpenUBL",
    "codigoPostal": "050101"
  },
  "cliente": {
    "tipoDocumentoIdentidad": "RUC",
    "numeroDocumentoIdentidad": "12312312312",
    "nombre": "Nombre de mi cliente"
  },
  "detalle": [
    {
      "descripcion": "Nombre de producto o servicio",
      "precioUnitario": 1,
      "cantidad": 1,
      "tipoIGV": "EXONERADO_TRANSFERENCIA_GRATUITA"
    }
  ]
}
```

XML resultado:

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<Invoice xmlns="urn:oasis:names:specification:ubl:schema:xsd:Invoice-2"
        xmlns:cac="urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2"
        xmlns:cbc="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2"
        xmlns:ccts="urn:un:unece:uncefact:documentation:2"
        xmlns:cec="urn:oasis:names:specification:ubl:schema:xsd:CommonExtensionComponents-2"
        xmlns:ds="http://www.w3.org/2000/09/xmldsig#"
        xmlns:ext="urn:oasis:names:specification:ubl:schema:xsd:CommonExtensionComponents-2"
        xmlns:qdt="urn:oasis:names:specification:ubl:schema:xsd:QualifiedDatatypes-2"
        xmlns:sac="urn:sunat:names:specification:ubl:peru:schema:xsd:SunatAggregateComponents-1"
        xmlns:udt="urn:un:unece:uncefact:data:specification:UnqualifiedDataTypesSchemaModule:2"
        xmlns:xs="http://www.w3.org/2001/XMLSchema"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>
    <ext:UBLExtensions>
        <ext:UBLExtension>
            <ext:ExtensionContent/>
        </ext:UBLExtension>
    </ext:UBLExtensions>
    <cbc:UBLVersionID>2.1</cbc:UBLVersionID>
    <cbc:CustomizationID>2.0</cbc:CustomizationID>
    <cbc:ID>F001-1</cbc:ID>
    <cbc:IssueDate>2020-02-17</cbc:IssueDate>
    <cbc:IssueTime>16:26:18</cbc:IssueTime>
    <cbc:InvoiceTypeCode listID="0101" listAgencyName="PE:SUNAT" listName="SUNAT:Identificador de Tipo de Documento" listURI="urn:pe:gob:sunat:cpe:see:gem:catalogos:catalogo01">01</cbc:InvoiceTypeCode>
    <cbc:DocumentCurrencyCode listID="ISO 4217 Alpha" listAgencyName="United Nations Economic Commission for Europe" listName="Currency">PEN</cbc:DocumentCurrencyCode>
    <cbc:LineCountNumeric>1</cbc:LineCountNumeric>
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
        <cac:Party>
            <cac:PartyIdentification>
                <cbc:ID schemeID="6" schemeAgencyName="PE:SUNAT" schemeName="SUNAT:Identificador de Documento de Identidad" schemeURI="urn:pe:gob:sunat:cpe:see:gem:catalogos:catalogo06">12345678912</cbc:ID>
            </cac:PartyIdentification>
            <cac:PartyLegalEntity>
                <cbc:RegistrationName><![CDATA[Project OpenUBL]]></cbc:RegistrationName>
                <cac:RegistrationAddress>
                    <cbc:AddressTypeCode>050101</cbc:AddressTypeCode>
                </cac:RegistrationAddress>
            </cac:PartyLegalEntity>
        </cac:Party>
    </cac:AccountingSupplierParty>
    <cac:AccountingCustomerParty>
        <cac:Party>
            <cac:PartyIdentification>
                <cbc:ID schemeID="6" schemeAgencyName="PE:SUNAT" schemeName="SUNAT:Identificador de Documento de Identidad" schemeURI="urn:pe:gob:sunat:cpe:see:gem:catalogos:catalogo06">12312312312</cbc:ID>
            </cac:PartyIdentification>
            <cac:PartyLegalEntity>
                <cbc:RegistrationName><![CDATA[Nombre de mi cliente]]></cbc:RegistrationName>
            </cac:PartyLegalEntity>
        </cac:Party>
    </cac:AccountingCustomerParty>
    <cac:TaxTotal>
        <cbc:TaxAmount currencyID="PEN">0</cbc:TaxAmount>
        <cac:TaxSubtotal>
            <cbc:TaxableAmount currencyID="PEN">1</cbc:TaxableAmount>
            <cbc:TaxAmount currencyID="PEN">0</cbc:TaxAmount>
            <cac:TaxCategory>
                <cbc:ID schemeAgencyName="United Nations Economic Commission for Europe" schemeID="UN/ECE 5305" schemeName="Tax Category Identifie">S</cbc:ID>
                <cac:TaxScheme>
                    <cbc:ID schemeAgencyName="PE:SUNAT" schemeID="UN/ECE 5153" schemeName="Codigo de tributos">9996</cbc:ID>
                    <cbc:Name>GRA</cbc:Name>
                    <cbc:TaxTypeCode>FRE</cbc:TaxTypeCode>
                </cac:TaxScheme>
            </cac:TaxCategory>
        </cac:TaxSubtotal>
    </cac:TaxTotal>
    <cac:LegalMonetaryTotal>
        
        
        <cbc:AllowanceTotalAmount currencyID="PEN">0</cbc:AllowanceTotalAmount>
        <cbc:ChargeTotalAmount currencyID="PEN">0</cbc:ChargeTotalAmount>
        <cbc:PayableAmount currencyID="PEN">0</cbc:PayableAmount>
    </cac:LegalMonetaryTotal>
    <cac:InvoiceLine>
        <cbc:ID>1</cbc:ID>
        <cbc:InvoicedQuantity unitCode="NIU" unitCodeListAgencyName="United Nations Economic Commission for Europe" unitCodeListID="UN/ECE rec 20">1</cbc:InvoicedQuantity>
        <cbc:LineExtensionAmount currencyID="PEN">1</cbc:LineExtensionAmount>
        <cac:PricingReference>
            <cac:AlternativeConditionPrice>
                <cbc:PriceAmount currencyID="PEN">1</cbc:PriceAmount>
                <cbc:PriceTypeCode listAgencyName="PE:SUNAT" listName="SUNAT:Indicador de Tipo de Precio" listURI="urn:pe:gob:sunat:cpe:see:gem:catalogos:catalogo16">02</cbc:PriceTypeCode>
            </cac:AlternativeConditionPrice>
        </cac:PricingReference>
        <cac:TaxTotal>
            <cbc:TaxAmount currencyID="PEN">0</cbc:TaxAmount>
            <cac:TaxSubtotal>
                <cbc:TaxableAmount currencyID="PEN">1</cbc:TaxableAmount>
                <cbc:TaxAmount currencyID="PEN">0</cbc:TaxAmount>
                <cac:TaxCategory>
                    <cbc:ID schemeAgencyName="United Nations Economic Commission for Europe" schemeID="UN/ECE 5305" schemeName="Tax Category Identifier">S</cbc:ID>
                    <cbc:Percent>0</cbc:Percent>
                    <cbc:TaxExemptionReasonCode listAgencyName="PE:SUNAT" listName="SUNAT:Codigo de Tipo de Afectacion del IGV" listURI="urn:pe:gob:sunat:cpe:see:gem:catalogos:catalogo07">21</cbc:TaxExemptionReasonCode>
                    <cac:TaxScheme>
                        <cbc:ID schemeAgencyName="PE:SUNAT" schemeID="UN/ECE 5153" schemeName="Codigo de tributos">9996</cbc:ID>
                        <cbc:Name>GRA</cbc:Name>
                        <cbc:TaxTypeCode>FRE</cbc:TaxTypeCode>
                    </cac:TaxScheme>
                </cac:TaxCategory>
            </cac:TaxSubtotal>
        </cac:TaxTotal>
        <cac:Item>
            <cbc:Description><![CDATA[Nombre de producto o servicio]]></cbc:Description>
        </cac:Item>
        <cac:Price>
            <cbc:PriceAmount currencyID="PEN">0</cbc:PriceAmount>
        </cac:Price>
    </cac:InvoiceLine>
</Invoice>
```