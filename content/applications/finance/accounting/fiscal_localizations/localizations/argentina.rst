=========
Argentina
=========

Webinars
========

Below you can find videos with a general description of the localization, and how to configure it.

- `VIDEO WEBINAR V15 <https://www.youtube.com/watch?v=_H1HbU-wKVg>`_.
- `VIDEO WEBINAR ECOMMERCE <https://www.youtube.com/watch?v=5gUi2WWfRuI>`_.

Introduction
============

The following modules are necessary for all databases that require Argentinian localization:

- **l10n_ar**: This module adds accounting features for the Argentinian localization, which
  represent the minimal configuration needed for a company  to operate in Argentina and under the
  AFIP (Administración Federal de Ingresos Públicos) regulations and guidelines.

- **l10n_ar_reports**: Add VAT Book report which is a legal requirement in Argentine and that holds
  the VAT detail info of sales or purchases recorded on the journal entries. This module includes as
  well the VAT summary report that is used to analyze the invoice.
  
- **l10n_ar_edi**: This module includes all technical and functional requirements to generate 
  Electronic Invoices via web service, based on the AFIP regulations. 

The following module is optional and should be installed only if it meets a specific organization
requirement.

- **l10n_ar_website_sale**: This module allows the user to see Identification Type and AFIP
  Responsibility in the eCommerce checkout form to create electronic invoices from there.

Configuration
=============

Install the Argentinian localization modules
--------------------------------------------

For this, go to :guilabel:`Apps` and search for Argentina. Then click :guilabel:`Install` for the
Argentinian Modules.

.. image:: argentina/install-argentinian-l10-modules.png
   :align: center
   :alt: Install Argentinian localization modules.

Configure your company
~~~~~~~~~~~~~~~~~~~~~~

Once that the modules are installed, the first step is to set up your company data. Additional to
the basic information, a key field to fill is the :guilabel:`AFIP Responsibility Type`, which
represents the fiscal obligation and structure of the company:

.. image:: argentina/select-responsibility-type.png
   :align: center
   :alt: Select AFIP Responsibility Type.
   
Chart of Account
~~~~~~~~~~~~~~~~

In Accounting, settings are available in three different packages of :guilabel:`Chart of Accounts`
to choose from, they are based on the company's AFIP responsibility type. Considering that if the
base companies don't require as many accounts as the companies that gave more complex fiscal
requirements:

- Monotributista (227 accounts).
- IVA Exento (290 accounts).
- Responsable Inscripto (298 Accounts).

.. image:: argentina/select-fiscal-package.png
   :align: center
   :alt: Select Fiscal Localization Package.

Configure Master data
---------------------

Electronic Invoice Credentials
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Environment
***********

The AFIP infrastructure is replicated in two separate environments, Testing and Production.

Testing is provided so that the Companies can test their databases until they are ready to move
into the Production environment. As these two environments are completely isolated from each other,
the digital certificates of one instance are not valid in the other one.

Go to :menuselection:`Accounting --> Settings --> Argentinian Localization` to select the
environment:

.. image:: argentina/select-environment.png
   :align: center
   :alt: Select Envorinment: Testing or Production.

AFIP Certificates
*****************

The electronic invoice and other AFIP services work with :guilabel:`WebServices (WS)` provided by
the AFIP.

In order to enable communication with the AFIP, the first step is to request a
:guilabel:`Digital Certificate` if you don't have one already.   

#. :guilabel:`Generate certificate Sign Request (Odoo)`. When this option is selected a file with
   extension ``.csr`` (certificate signing request) is generated to be used the AFIP portal to
   request the certificate.

   .. image:: argentina/request-certificate.png
      :align: center
      :alt: Request a certificate.

#. :guilabel:`Generate Certificate (AFIP)`. Access the AFIP portal and follow the instructions
   described in the next document to get a certificate. `Get AFIP Certificate
   <http://www.afip.gob.ar/ws/WSAA/wsaa_obtener_certificado_produccion.pdf>`_.
   
#. :guilabel:`Upload Certificate and Private Key (Odoo)`. Once the certificate has been generated,
   it needs to be uploaded in Odoo using the pencil next to the field “Certificado” and selecting
   the corresponding file.

   .. image:: argentina/upload-certificate-private-key.png
      :align: center
      :alt: Upload Certificate and Private Key.

.. tip::
   In case you need to configure the Homologation Certificate, please refer to the AFIP official
   documentation: `Homologation Certificate
   <http://www.afip.gob.ar/ws/documentacion/certificados.asp>`_. Furthermore, Odoo allows the user
   to test electronic invoicing locally without a Homologation Certificate. The following message
   will be in the chatter when testing locally:

   .. image:: argentina/local-testing.png
      :align: center
      :alt: Local testing.

Partner
~~~~~~~

Identification Type and VAT
***************************

As part of the Argentinian localization, the document types defined by the AFIP are now available
on the Partner form, this information is essential for most transactions. There are 6
identification types available by default plus 32 inactive:

.. image:: argentina/identification-types.png
   :align: center
   :alt: Identification types.

.. note::
   The complete list of Identification types defined by the AFIP is included in Odoo but only the
   common ones are active.

AFIP Responsibility Type
************************

In Argentina the document type associated with customers and vendors, and transactions is defined
based on the AFIP Responsibility type, this field should be defined in the partner form:

.. image:: argentina/select-afip-responsibility-type.png
   :align: center
   :alt: Select AFIP Responsibility Type.

Taxes
~~~~~

As part of the localization module, the taxes are created automatically with their related
financial account and configuration. e.g. 73 taxes for “Responsable Inscripto”:

.. image:: argentina/automatic-tax-configuration.png
   :align: center
   :alt: Taxes.

Taxes Types
***********

Argentina has several tax types, the most common ones are:

- :guilabel:`VAT`: This is the regular VAT and it can have several percentages.
- :guilabel:`Perception`: Advance payment of a tax that is applied on invoices.
- :guilabel:`Retention`: Advance payment of a tax that is applied on payments.

Special Taxes
*************

Some Argentine taxes are not commonly used for all companies, these type of taxes are included as
inactive by default, it's important to remember that before creating a new tax you confirm if they
are not already included in the Inactive taxes:

.. image:: argentina/special-inactive-taxes.png
   :align: center
   :alt: Special Taxes.

Document Types
~~~~~~~~~~~~~~

In some Latin America countries, including Argentina, some accounting transactions like invoices
and vendor bills are classified by document types defined by the government fiscal authorities
(AFIP in Argentina).

The document type is an essential information that needs to be displayed in the printed reports and
that needs to be easily identified, within the set of invoices as well of account moves.

Each document type can have a unique sequence per journal where it is assigned. As part of the
localization, the document type includes the country on which the document is applicable and the
data is created automatically when the localization module is installed.

The information required for the document types is included by default so the user doesn't need to
fill anything on this view:

.. image:: argentina/default-document-type-info.png
   :align: center
   :alt: Document types.

.. note::
   There are several document types that are inactive by default but can be activated if needed.

Letters
*******

For Argentina, the document types include a letter that helps that indicates the
transaction/operation, for example:

- When an invoice is related to a :guilabel:`B2B transaction`, a document type "A" must be used.
- When an invoice is related to a :guilabel:`B2C transaction`, a document type "B" must be used.
- When an invoice is related to :guilabel:`Exportation Transaction`, a document type "E" must be
  used.

The documents included in the localization have the proper letter associated, the user doesn't need
to configure anything else.

.. image:: argentina/document-types-grouped-by-letters.png
   :align: center
   :alt: Document types grouped by letters.

Use on Invoices
***************

The document type on each transaction will be determined by:

- The Journal related to the Invoice, identifying if the journal uses documents.
- Conditions applied based on the type of Issuer and Receiver (ex. Type of fiscal regimen of the
  buyer and type of fiscal regimen of the vendor)

Journals
--------

In the Argentinian localization the Journal can have a different approach depending on its usage
and internal type, to configure journals go to :menuselection:`Accounting --> Configuration -->
Journals`:

For Sales and Purchase Journals it's possible to enable the option :guilabel:`Use Documents`, this
indicates the Journal to enable a list of document types that can be related to the Invoices and
vendor Bills, for more detail of the invoices, please refer to the section 2.3 Document Types.

If the Sales/Purchase journal are used without the option :guilabel:`Use Documents`, they will not
be used to generate fiscal invoices, but mostly for account moves related to internal control
process.

AFIP Information (also known as AFIP Point of Sale)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: argentina/sales-journal.png
   :align: center
   :alt: Sales journal.

:guilabel:`AFIP POS System`: This field is only visible for the Sales journals and defined the type
of AFIP POS that will be used to manage the transactions for which the journal is created. The AFIP
POS defines as well:

#. The sequences of document types related to the Web service.
#. The structure and data of the electronic invoice file.

Web Services
************

- :guilabel:`wsfev1: Electronic Invoice`: This is the most common service, is used to generate 
  invoices for document types A, B, C, M  with no detail per item.
- :guilabel:`wsbfev1: Electronic Fiscal Bond`: For those who invoice capital goods and wish to
  access the benefit of the Electronic Tax Bonds granted by the Ministry of Economy. For more
  detail go to:
  `Fiscal Bond <https://www.argentina.gob.ar/acceder-un-bono-por-fabricar-bienes-de-capital>`__.
- :guilabel:`wsfexv1: Electronic Exportation Invoice`: Used to generate invoices for international
  customers and transactions that involve exportation process, the document type related is type
  “E”.

.. image:: argentina/web-services.png
   :align: center
   :alt: Web Services.

:guilabel:`AFIP POS Number`: This is the number configured in the AFIP to identify the operations
related to this AFIP POS.

:guilabel:`AFIP POS Address`: This field is related to commercial address registered for the POS,
which is usually the same address than the Company. For example: has multiple stores (fiscal
locations) then AFIP will require that you have one AFIP POS per location: this location will be
printed in the invoice report.

:guilabel:`Unified Book`: When AFIP POS System is Preimpresa the document types (applicable to the
journal) with the same letter will share the same sequence. For example:

- Invoice: FA-A 0001-00000002.
- Credit Note: NC-A 0001-00000003.
- Debit Note: ND-A 0001-00000004.

Sequences
~~~~~~~~~

For the first invoice, Odoo syncs with AFIP automatically and brings the last sequence used.

.. note::
   When creating the :guilabel:`Purchase Journals`, it's possible to define if they can be related
   to document types or not. In case the the option to use documents is selected, there is no need
   to manually associate the document type sequences as the document number is provided by the
   vendor.

Usage and testing
=================

Invoice
-------

Once the partners and journals are created and configured, when the invoices are created they will
have the next behaviour:

Document type assignation
~~~~~~~~~~~~~~~~~~~~~~~~~

Once the partner is selected the document type will filled automatically, based on the AFIP
document type:

**Invoice for a customer IVA Responsable Inscripto, prefix A**.

.. image:: argentina/prefix-a-invoice-for-customer.png
   :align: center
   :alt: Invoice for a customer IVA Responsable Inscripto, prefix A.

**Invoice for an end customer, prefix B**.

.. image:: argentina/prefix-b-invoice-for-end-customer.png
   :align: center
   :alt: Invoice for an end customer, prefix B.

**Exportation Invoice, prefix E**.

.. image:: argentina/prefix-e-exporation-invoice.png
   :align: center
   :alt: Exportation Invoice, prefix E 

Even though some invoices use the same journal, the prefix and sequence are given by the document
type.

The most common document type will be defined automatically for the different combinations of AFIP
responsibility type but it can be updated manually by the user before confirming the invoice.


Electronic Invoice elements
~~~~~~~~~~~~~~~~~~~~~~~~~~~

When using electronic invoice, if all the information is correct the Invoice is posted in the
standard way, in case something needs to be addressed (check the section common errors for more
detail), an error message is raised indicating the issue/proposed solution and the invoice remains
in draft until the related issue is corrected.

Once the invoice is posted, the information related to the AFIP validation and status is displayed
in the AFIP Tab, including:

- :guilabel:`AFIP Autorisation`: CAE number.
- :guilabel:`Expiration Date`: Deadline to deliver the invoice to the customers. Normally 10 days
  after the CAE is generated.
- :guilabel:`Result:`

  - Aceptado en AFIP.
  - Aceptado con Observaciones. 
  
.. image:: argentina/afip-status.png
   :align: center
   :alt: AFIP Status.

Invoice Taxes
~~~~~~~~~~~~~

Based on the :guilabel:`AFIP Responsibility type`, the VAT tax can have a different behavior on the
pdf report:

:guilabel:`A. Tax excluded:` In this case the taxed amount needs to be clearly identified in the
report. This condition applies when the customer has the following AFIP Responsibility type:

- Responsable Inscripto.

.. image:: argentina/tax-amount-excluded.png
   :align: center
   :alt: Tax excluded.

:guilabel:`B. Tax amount included:` This means that the taxed amount is included as part of the
product price, subtotal, and totals. This condition applies when the customer has the following
AFIP Responsibility types:

- IVA Sujeto Exento.
- Consumidor Final.
- Responsable Monotributo.
- IVA liberado.

.. image:: argentina/tax-amount-included.png
   :align: center
   :alt: Tax amount included.

Special Use Cases
~~~~~~~~~~~~~~~~~

Invoices for Services
*********************

For electronic invoices that include :guilabel:`Services`, the AFIP requires to report the service
starting and ending date, this information can be filled in the tab :guilabel:`Other Info`: 

.. image:: argentina/invoices-for-services.png
   :align: center
   :alt: Invoices for Services.

If the dates are not selected manually before the invoice is validated, the values will be
filled automatically with the first and last day of the invoice's month:

.. image:: argentina/service-dates.png
   :align: center
   :alt: Service Dates.

Exportation Invoices
********************

The invoices related to :guilabel:`Exportation Transactions` required a Journal that used the AFIP
POS System “Expo Voucher - Web Service” so the proper document type be associated:

.. image:: argentina/exporation-journal.png
   :align: center
   :alt: Exporation journal.

When the customer selected in the Invoice has set the AFIP responsibility type as 
:guilabel:`Cliente / Proveedor del Exterior` or :guilabel:`IVA Liberado - Ley Nº 19.640`, Odoo
automatically assigned:

- Journal related to the exportation Web Service.
- Exportation document type .
- Fiscal position: Compras/Ventas al exterior.
- Concepto AFIP:  Products / Definitive export of goods.
- Exempt Taxes. 

.. image:: argentina/export-invoice.png
   :align: center
   :alt: Export invoice.

.. note::
   The Exportation Documents required the Incoterm in :menuselection:`Other Info --> Accounting`:
   
.. image:: argentina/export-invoice-incoterm.png
   :align: center
   :alt: Export invoice - Incoterm
   
Fiscal Bond
***********

The :guilabel:`Electronic Fiscal Bond` is used for those who invoice capital goods and wish to
access the benefit of the Electronic Tax Bonds granted by the Ministry of Economy.

For these transactions it's important to consider the following requirements:

- Currency (according to parameter table) and invoice quotation.
- Taxes.
- Zone.
- Detail each item.

  - Code according to the Common Nomenclator of Mercosur (NCM).
  - Complete description.
  - Unit Net Price.
  - Quantity.
  - Unit of measurement.
  - Bonus.
  - VAT rate.

Electronic Credit Invoice MiPyme (FCE) 
**************************************

:guilabel:`Invoices:` There are several document types classified as Mipyme also known as
Electronic Credit Invoice (FCE in spanish), which is used to foster the SME, its purpose is 
to develop a mechanism that improves the financing conditions of these companies and allows 
them to increase their productivity, through the early collection of credits and receivables 
issued to their clients and / or vendors. 

For these transactions it's important to have consider the next requirements:

- Specific document types (201, 202, 206, etc).
- The emisor should be eligible by the AFIP to MiPyme transactions. 
- The amount should be bigger than 100,000 ARS. 
- A bank account type CBU must be related to the emisor, otherwise the invoice can't
  be validated, having these errors messages for example:

.. image:: argentina/argentina_edi_10.png
   :align: center
   :alt: Bank account relation error.

To set up the :guilabel:`Transmission Mode` go to settings and select one of those (SDC or ADC):

.. image:: argentina/transmission-mode.png
   :align: center
   :alt: Transmission Mode.

To change the :guilabel:`Transmission Mode` for a specific invoice, go to the
:guilabel:`Other Info` tab and change it before confirming (The mode selected in settings will not
be changed):

.. image:: argentina/transmission-mode-on-invoice.png
   :align: center
   :alt: Transmission Mode on Invoice.

:guilabel:`Credit& Debit Notes:` When creating a :guilabel:`Credit/Debit` note related to a FCE
document, it is important to consider the next points:

- Use the :guilabel:`Credit and Debit Note` buttons, so the correct reference of the originator
  document passed to the note.

.. image:: argentina/credit-debit-notes-button.png
   :align: center
   :alt: Credit & debit notes buttons.
   
- The document letter should be the same than the originator document (either A or B).
- The same currency as the source document must be used.  When using a secondary currency
  there is an exchange difference  if the currency rate is different between the emission day
  and the payment date, so it's possible to create a credit/debit note to decrease/increase the
  amount to pay in ARS.

In the workflow we can have two scenarios:

#. The FCE is rejected so the :guilabel:`Credit Note` should have the field
   :guilabel:`FCE, is Cancellation?` as *True*. 
#. The :guilabel:`Credit Note`, is created annul the FCE document, in this case the field
   :guilabel:`FCE, is Cancellation?` must be *empty* (false).

.. image:: argentina/fce-es-cancelation.png
   :align: center
   :alt: FCE: Es Cancelación?
   
Invoice printed report
~~~~~~~~~~~~~~~~~~~~~~

The :guilabel:`PDF Report` related to electronic invoices that have been validated by the AFIP
includes a barcode at the bottom of the format which represent the CAE number, the Expiration Date
is also displayed as it's legal requirement:
   
.. image:: argentina/invoice-printed-report.png
   :align: center
   :alt: Invoice printed report.

Troubleshooting and Auditing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For auditing and troubleshooting purposes you can get the detailed information of an invoice number
that has been previously sent to the AFIP. To get it go into 
:doc:`Developer Mode <../../../../general/developer_mode>`, then go to the accounting menu and
then click in the button :guilabel:`Consult Invoice` in AFIP:

.. image:: argentina/consult-invoice-in-afip.png
   :align: center
   :alt: Consult invoice in AFIP.
     
.. image:: argentina/consult-invoice-in-afip-details.png
   :align: center  
   :alt: Details of invoice consulted in AFIP.

You can also get the last number used in AFIP for a specific Document Type and POS Number 
as reference for any possible issues on the sequence synchronization between Odoo and AFIP. 

.. image:: argentina/consult-last-invoice-number.png
   :align: center
   :alt: Consult the last invoice number.

Vendor Bills
------------

Based on the purchase journal selected for the vendor bill, the document type is now a required
field. This value is auto populated based on the AFIP Responsibility type of Issuer and Customer,
but the value can be switched if necessary.

.. image:: argentina/changing-journal-document-type.png
   :align: center
   :alt: Changing journal and document type

The document number needs to be registered manually and the format is validated automatically, in
case the format is invalid a user error will be displayed indicating the correct format that is
expected.

.. image:: argentina/vendor-bill-document-number.png
   :align: center
   :alt: Vendor bill document number.

The vendor bill number is structured in the same way as the customer invoices with the difference
that the document sequence is entered by the user using the next format:
*"Document Prefix - Letter - Document number".*

Validate Vendor Bill number in AFIP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As most companies have internal controls to verify that the vendor bill is related to an AFIP
valid document, an automatic validation can be set in :menuselection:`Accounting --> Settings --> 
Argentinian Localization --> Validate document in the AFIP`, considering the following levels: 

- :guilabel:`Not available:` The verification is not done (this is the default value).
- :guilabel:`Available:` The verification is done, in case the number is not valid it only raises a
  warning but it allows you to post the vendor bill.
- :guilabel:`Required:` The verification is done and it doesn't allow the user to post the vendor
  bill if the document number is not valid.

.. image:: argentina/verify-vendor-bills.png
   :align: center
   :alt: Verify Vendor Bills validity in AFIP.

How to use it in Odoo
*********************

This tool incorporates in the vendor bill a new :guilabel:`Verify on AFIP` button located next to
the :guilabel:`AFIP Authorization code`. 

.. image:: argentina/verify-on-afip.png
   :align: center
   :alt: Verify on AFIP.

In case it's not a valid AFIP authorization the value :guilabel:`Rejected` will be displayed and
the details of the validation will be added to the chatter.

.. image:: argentina/afip-auth-rejected.png
   :align: center
   :alt: AFIP authorization Rejected.

Special Use cases
~~~~~~~~~~~~~~~~~

Untaxed Concepts
****************

There are some transactions that include items that are not part of the VAT base amount, this is
commonly used in fuel and gasoline invoices. 

The vendor bill will be registered using 1 item for each product that is part of the VAT base
amount and an additional item to register the amount of the Exempt concept:

.. image:: argentina/vat-exempt.png
   :align: center
   :alt: VAT exempt.

Perception Taxes
****************

The vendor bill will be registered using 1 item for each product that is part of the VAT base
amount, the perception tax can be added in any of the product lines, as result we will have one
tax group for the VAT and one for the perception, the perception default value is always
:guilabel:`0.10`.

.. image:: argentina/vat-perception.png
   :align: center
   :alt: VAT perception.

To edit it and set the correct amount you should use the :guilabel:`Pencil` that is the next to the
Perception amount.

.. image:: argentina/enter-perception-amount.png
   :align: center
   :alt: Enter the perception amount.
   
Then invoice can be validated.
   
Reports
=======

As part of the localization the next Financial reports were added:

.. image:: argentina/argentinian-reports.png
   :align: center
   :alt: Argentinian reports.

VAT Reports
-----------

Sales VAT book
~~~~~~~~~~~~~~

.. image:: argentina/sales-vat-book.png
   :align: center
   :alt: Sales VAT book.

The :guilabel:`Sales VAT` book report can be exported in a Zip file :guilabel:`VAT BOOK (ZIP)`
button in the top left, which contains TXT files to upload in the AFIP portal.

Purchases VAT book
~~~~~~~~~~~~~~~~~~

.. image:: argentina/purchases-vat-book.png
   :align: center
   :alt: Purchases VAT book.

The :guilabel:`Purchases VAT` book report can be exported in a Zip file :guilabel:`VAT BOOK (ZIP)`
button in the top left, which contains TXT files to upload in the AFIP portal.

VAT Summary
~~~~~~~~~~~

.. image:: argentina/vat-summary.png
   :align: center
   :alt: VAT Summary.

IIBB - Reports
--------------

IIBB - Sales by jurisdiction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: argentina/iibb-sales-jurisdiction.png
   :align: center
   :alt: IIBB Sales by jurisdiction.

IIBB - Purchases by jurisdiction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: argentina/iibb-purchases-jurisdiction.png
   :align: center
   :alt: IIBB Purchases by jurisdiction.