<?xml version="1.0"?>
<!DOCTYPE pdf PUBLIC "-//big.faceless.org//report" "report-1.1.dtd">
<pdf>
  <head>
    <link name="NotoSans" type="font" subtype="truetype" src="${nsfont.NotoSans_Regular}" src-bold="${nsfont.NotoSans_Bold}" src-italic="${nsfont.NotoSans_Italic}" src-bolditalic="${nsfont.NotoSans_BoldItalic}" bytes="2" />
    <#if .locale=="zh_CN">
      <link name="NotoSansCJKsc" type="font" subtype="opentype" src="${nsfont.NotoSansCJKsc_Regular}" src-bold="${nsfont.NotoSansCJKsc_Bold}" bytes="2" />
      <#elseif .locale=="zh_TW">
        <link name="NotoSansCJKtc" type="font" subtype="opentype" src="${nsfont.NotoSansCJKtc_Regular}" src-bold="${nsfont.NotoSansCJKtc_Bold}" bytes="2" />
        <#elseif .locale=="ja_JP">
          <link name="NotoSansCJKjp" type="font" subtype="opentype" src="${nsfont.NotoSansCJKjp_Regular}" src-bold="${nsfont.NotoSansCJKjp_Bold}" bytes="2" />
          <#elseif .locale=="ko_KR">
            <link name="NotoSansCJKkr" type="font" subtype="opentype" src="${nsfont.NotoSansCJKkr_Regular}" src-bold="${nsfont.NotoSansCJKkr_Bold}" bytes="2" />
            <#elseif .locale=="th_TH">
              <link name="NotoSansThai" type="font" subtype="opentype" src="${nsfont.NotoSansThai_Regular}" src-bold="${nsfont.NotoSansThai_Bold}" bytes="2" />
    </#if>
    <macrolist style="margin-top:1000px;">
<macro id="nlheader" style="margin-top:1000px;">
<table style="width: 100%; border-collapse: collapse;">
  <tr>

    <!-- LEFT: Tax Invoice + IRN/Ack details — 70% width -->
    <td style="width: 70%; vertical-align: top;">
      <table style="width: 100%; border-collapse: collapse;">

        <!-- Tax Invoice Title -->
        <tr>
          <td colspan="2" align="right"
              style="text-align: right; padding: 8px 5px 4px 5px;
                     font-size: 14px; font-weight: bold;margin-right:20px;">
            Tax Invoice
          </td>
        </tr>

        <!-- LUT Bond notice — sirf tab dikhao -->
        <#if record.custbody_in_gst_lut_bond_number?has_content>
        <tr>
          <td colspan="2" align="center"
              style="text-align: center; font-size: 10px; padding: 2px 5px;">
            (SUPPLY MEANT FOR EXPORT/SUPPLY TO SEZ UNIT OR SEZ DEVELOPER FOR<br/>
             AUTHORISED OPERATIONS UNDER BOND OR LETTER OF UNDERTAKING<br/>
             WITHOUT PAYMENT OF IGST)
          </td>
        </tr>
        </#if>

        <!-- IRN -->
        <tr>
          <td style="font-size: 10px; padding: 2px 5px; white-space: nowrap; width: 60px;">
            IRN:
          </td>
          <td style="font-size: 10px; padding: 2px 5px;margin-left:0px">
            <b>${record.custbody_ageinv_irnno!''}</b>
          </td>
        </tr>

        <!-- Ack No -->
        <tr>
          <td style="font-size: 10px; padding: 2px 5px; white-space: nowrap;">
            Ack No.:
          </td>
          <td style="font-size: 10px; padding: 2px 5px,margin-left:0px;">
            <b>${record.custbody_ageinv_ackno!''}</b>
          </td>
        </tr>

        <!-- Ack Date -->
        <tr>
          <td style="font-size: 10px; padding: 2px 5px 4px 5px; white-space: nowrap;">
            Ack Date:
          </td>
          <td style="font-size: 10px; padding: 2px 5px 4px 5px;">
            <#assign ackDateStr = record.custbody_ageinv_ackdt!''>
            <#if ackDateStr?has_content && (ackDateStr?length == 19)>
              <b>${ackDateStr?datetime("yyyy-MM-dd HH:mm:ss")?string("dd-MMM-yy HH:mm:ss")}</b>
            <#elseif ackDateStr?has_content>
              <b>${ackDateStr}</b>
            </#if>
          </td>
        </tr>

      </table>
    </td>

    <!-- RIGHT: Logo + QR — 30% width -->
    <td style="width: 30%; vertical-align: top; text-align: right; padding: 4px 4px 0 0;">

      <!-- Logo — fixed pixels only, no percentage -->
      <#if companyInformation.logoUrl?has_content>
        <img src="${companyInformation.logoUrl}"
             style="height: 55px; width: 110px;"/>
      </#if>

      <!-- QR Code — sirf tab jab IRN ho -->
      <#if record.custbody_ageinv_irnno?has_content>
        <br/>
        <span style="font-size: 9px; font-weight: bold;">e-Invoice</span><br/>
        <barcode codetype="qrcode" height="80px" width="80px" showtext="false"
                 value="${record.custbody_ageinv_signedqrcode!''}"/>
      <#elseif record.custbody_in_ei_irn?has_content>
        <br/>
        <span style="font-size: 9px; font-weight: bold;">e-Invoice</span><br/>
        <barcode codetype="qrcode" height="80px" width="80px" showtext="false"
                 value="${record.custbody_in_ei_irn!''}"/>
      </#if>

    </td>

  </tr>
</table>

  <#assign names = [
    {"shortName": "01-JK", "fullName": "Jammu &amp; Kashmir"},
    {"shortName": "02-HP", "fullName": "Himachal Pradesh"},
    {"shortName": "03-PB", "fullName": "Punjab"},
    {"shortName": "04-CH", "fullName": "Chandigarh"},
    {"shortName": "05-UK", "fullName": "Uttarakhand"},
    {"shortName": "06-HR", "fullName": "Haryana"},
    {"shortName": "07-DL", "fullName": "Delhi"},
    {"shortName": "08-RJ", "fullName": "Rajasthan"},
    {"shortName": "09-UP", "fullName": "Uttar Pradesh"},
    {"shortName": "10-BR", "fullName": "Bihar"},
    {"shortName": "11-SK", "fullName": "Sikkim"},
    {"shortName": "12-AR", "fullName": "Arunachal Pradesh"},
    {"shortName": "13-NL", "fullName": "Nagaland"},
    {"shortName": "14-MN", "fullName": "Manipur"},
    {"shortName": "15-MZ", "fullName": "Mizoram"},
    {"shortName": "16-TR", "fullName": "Tripura"},
    {"shortName": "17-ML", "fullName": "Meghalaya"},
    {"shortName": "18-AS", "fullName": "Assam"},
    {"shortName": "19-WB", "fullName": "West Bengal"},
    {"shortName": "20-JH", "fullName": "Jharkhand"},
    {"shortName": "21-OD", "fullName": "Odisha"},
    {"shortName": "22-CG", "fullName": "Chhattisgarh"},
    {"shortName": "23-MP", "fullName": "Madhya Pradesh"},
    {"shortName": "24-GJ", "fullName": "Gujarat"},
    {"shortName": "25-DD", "fullName": "Daman &amp; Diu"},
    {"shortName": "26-DN", "fullName": "Dadra &amp; Nagar Haveli"},
    {"shortName": "27-MH", "fullName": "Maharashtra"},
    {"shortName": "29-KA", "fullName": "Karnataka"},
    {"shortName": "30-GA", "fullName": "Goa"},
    {"shortName": "31-LD", "fullName": "Lakshdweep"},
    {"shortName": "32-KL", "fullName": "Kerala"},
    {"shortName": "33-TN", "fullName": "Tamil Nadu"},
    {"shortName": "34-PY", "fullName": "Pondicherry"},
    {"shortName": "35-AN", "fullName": "Andaman &amp; Nicobar Islands"},
    {"shortName": "36-TS", "fullName": "Telangana"},
    {"shortName": "37-AD", "fullName": "Andhra Pradesh"},
    {"shortName": "38-LA", "fullName": "Ladakh"},
    {"shortName": "97-OT", "fullName": "Other Territory"},
    {"shortName": "99-OC", "fullName": "Other Countries"}
  ]>

<#function processShipAddress shipAddress>
  <#assign shipAddress = shipAddress?replace("<br />", " ")>
  <#assign lines = shipAddress?split(" ")>
  <#assign extractedStateCode = "">
  <#list lines as line>
    <#list line?split(" ") as word>
      <#if word?matches("\\d{2}-[A-Z]{2}")>
        <#assign extractedStateCode = word?trim>
      </#if>
    </#list>
  </#list>
  <#list names as name>
    <#if name.fullName == extractedStateCode || name.shortName == extractedStateCode>
      <#return name.fullName>
    </#if>
  </#list>
  <#return extractedStateCode>
</#function>
<!-- Seller + Buyer + Invoice details table -->
<table class="submain">
  <tr>
    <!-- LEFT: Seller info + Buyer info -->
    <td style="border-right: 1px solid #000;">
      <table class="leftsection" style="height:100%; width:100%;">

        <!-- Seller Info -->
        <tr style="border-bottom: 1px solid #000;">
          <td style="padding: 0;">
            <p style="padding-left:5px; padding-top:5px; line-height:13px; font-size:10px;">
              <strong>${Subsidiary.legalname}</strong>
              <#if Subsidiary.addr1?has_content><br/>${Subsidiary.addr1}</#if>
              <#if Subsidiary.addr2?has_content><br/>${Subsidiary.addr2}</#if>
              <#if Subsidiary.zip?has_content><br/>${Subsidiary.zip}</#if>
              <br/>Country : ${Subsidiary.country!''}
              <br/>Telephone : ${Subsidiary.addrphone!''}
              <br/>GSTIN/UIN :
              <#assign companygst = record.subsidiarytaxregnum?split(" ")>
              ${companygst[0]}

              <#assign subAddrText = Subsidiary.addrtext!''>
              <#assign extractedState = "">
              <#list subAddrText?split(" ") as word>
                <#if word?trim?matches("\\d{2}-[A-Z]{2}")>
                  <#assign extractedState = word?trim>
                </#if>
              </#list>

              <#assign stateNumCode = "">
              <#assign stateFullName = "">
              <#if extractedState?has_content>
                <#assign dashIndex = extractedState?index_of("-")>
                <#assign stateNumCode = extractedState?substring(0, dashIndex)?trim>
                <#assign stateShortCode = extractedState?substring(dashIndex + 1)?trim>
                <#list names as name>
                  <#if name.shortName?contains("-" + stateShortCode)>
                    <#assign stateFullName = name.fullName>
                  </#if>
                </#list>
              </#if>

              <br/>State Name : ${stateFullName} , Code : ${stateNumCode}
              <br/>CIN :
            </p>
          </td>
        </tr>

        <!-- Buyer Info -->
        <tr style="height: 80px;">
          <td style="padding-top: 5px;">
            <p style="padding-left:5px; padding-top:2px; line-height:13px; font-size:10px;">
              <span style="font-weight:bold;">Buyer (Bill to)</span><br/>
              ${record.billaddress?replace("<br />"," ","r")}
            </p>
            <p style="padding-left:5px; font-size:10px;">
              Place of Supply: ${record.custbody_in_gst_pos!''}
            </p>
          </td>
        </tr>

      </table>
    </td>

    <!-- RIGHT: Invoice details grid -->
    <td style="width: 50%; padding: 0px; vertical-align: top;">
      <table class="rightsection">

        <tr style="border-bottom: 1px solid #000; height: 28px;">
          <td style="border-right:1px solid #000;">
            <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
              Invoice No.<br/><b>${record.tranid}</b>
            </p>
          </td>
          <td>
            <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
              Dated<br/><b>${record.trandate?string("dd-MMM-yy")}</b>
            </p>
          </td>
        </tr>

        <tr style="border-bottom: 1px solid #000; height: 28px;">
          <td style="border-right:1px solid #000;">
            <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
              Delivery Note<br/><b></b>
            </p>
          </td>
          <td>
            <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
              Mode/Terms of Payment:<br/>
              ${record.terms?has_content?then(record.terms,'Due on receipt')}
            </p>
          </td>
        </tr>

        <tr style="border-bottom: 1px solid #000; height: 28px;">
          <td style="border-right:1px solid #000;">
            <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
              Reference No. &amp; Date:<br/>
              <#if record.otherrefnum?has_content>
                <b>${record.otherrefnum} dt.${record.trandate?string("dd-MMM-yy")}</b>
              </#if>
            </p>
          </td>
          <td>
            <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
              Other References<br/><b></b>
            </p>
          </td>
        </tr>

        <tr style="border-bottom: 1px solid #000; height: 28px;">
          <td style="border-right:1px solid #000;">
            <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
              Buyer's Order No.<br/>
            </p>
          </td>
          <td>
            <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
              Dated<br/><b></b>
            </p>
          </td>
        </tr>

        <tr style="border-bottom: 1px solid #000; height: 28px;">
          <td style="border-right:1px solid #000;">
            <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
              Dispatch Doc No.<br/><b></b>
            </p>
          </td>
          <td>
            <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
              Delivery Note Date<br/><b></b>
            </p>
          </td>
        </tr>

        <tr style="border-bottom: 1px solid #000; height: 28px;">
          <td style="border-right:1px solid #000;">
            <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
              Dispatched through<br/><b></b>
            </p>
          </td>
          <td>
            <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
              Destination<br/>
              <b>${record.shippingaddress.country!''}</b>
            </p>
          </td>
        </tr>

        <tr style="height: 50px;">
          <td colspan="2" style="font-size:10px;">
            <p style="font-size:10px; padding: 2px 3px;">
              Terms of Delivery
            </p>
          </td>
        </tr>

      </table>
    </td>
  </tr>
</table>
</macro>

      <macro id="nlfooter">
        <table class="footer" style="width: 100%;">
          <!-- <#if subsidiary.internalid == "1">
          <tr>
            <td colspan="20" align="center">SUBJECT TO MUMBAI JURISDICTION <br/><br/></td>
          </tr>
          </#if> -->
          <tr>
            <td colspan="20" align="center"> This is Computer Generated INVOICE </td>
          </tr>
        </table>
      </macro>
    </macrolist>
    <style>
      * {
        <#if .locale=="zh_CN">font-family: NotoSans, NotoSansCJKsc, sans-serif;
        <#elseif .locale=="zh_TW">font-family: NotoSans, NotoSansCJKtc, sans-serif;
        <#elseif .locale=="ja_JP">font-family: NotoSans, NotoSansCJKjp, sans-serif;
        <#elseif .locale=="ko_KR">font-family: NotoSans, NotoSansCJKkr, sans-serif;
        <#elseif .locale=="th_TH">font-family: NotoSans, NotoSansThai, sans-serif;
        <#else>font-family: NotoSans, sans-serif;
        </#if>
      }

      table {
        table-layout: fixed;
      }

      th {
        font-weight: bold;
        vertical-align: middle;
        padding: 5px 6px 3px;
        color: #333333;
      }

      body {
        font-size: 10px;
      }

      b {
        font-weight: bold;
        color: #333333;
      }

      table.header td {
        padding: 0px;
      }

      table.footer td {
        padding: 0px;
      }

      table.itemtable th {
        padding-bottom: 10px;
        padding-top: 10px;
      }

      table.body td {
        padding-top: 2px;
      }

      table.total {
        page-break-inside: avoid;
      }

      tr.totalrow {
        line-height: 200%;
      }

      td.addressheader {
        padding-top: 6px;
        padding-bottom: 2px;
      }

      td.address {
        padding-top: 0px;
      }

      td.totalboxbot {
        font-weight: bold;
      }

      span.title {
        font-size: 16pt;
        font-weight: bold;
        font-family: sans-serif;
      }

      span.number {
        font-size: 16pt;
      }

      span.itemname {
        font-weight: bold;
        line-height: 150%;
      }

      hr {
        width: 100%;
        height: 1px;
      }

      .left-section {
        width: 50%;
        font-size: 14px;
      }

      .right-section {
        width: 50%;
      }

      .bold {
        font-weight: bold;
      }

      .section-title {
        margin: 0;
        font-size: 1.1em;
        text-decoration: underline;
      }

      .data-table {
        width: 100%;
        border-collapse: collapse;
        margin-top: 10px;
      }

      .data-table td {
        border: 1px solid black;
        padding: 5px;
        text-align: left;
      }

      .main {
        width: 100%;
        margin-top: 10px;
        overflow:hidden;
        border-collapse: collapse;
        line-height:10px;
      }

      .main td {
        width: 100%;
        padding: 0;
      }

      .submain {
        width: 100%;
        border: 1px solid #000;
        border-bottom:1px;
        border-collapse: collapse;
        font-size: 10px;
      }

      .submain td {
        width: 50%;
        vertical-align: top;
      }

      .leftsection {
        width: 100%;
        border-collapse: collapse;
        margin-top: 2px;
        font-family: sans-serif;
      }

      .leftsection tr {
        margin-top: 2px;
        font-size: 14px;
        font-family: sans-serif;
      }

      .rightsection {
        width: 100%;
        border-collapse: collapse;
      }

      .rightsection tr {
        font-family: sans-serif;
        height: 2%;
      }

      .rightsection td {
        padding: 2px;
        font-size: 12px;
        padding-bottom: 2px;
      }

      .itemtable {
        overflow:hidden;
        width:100%;
        height:300px;
      }

      #taxtable {
        width: 100%;
        margin-top: 0;
        border-collapse: collapse;
      }

      #taxtable td {
        border: 1px solid black;
      }
    </style>
  </head>

  <body header="nlheader" header-height="4.1in" footer="nlfooter" footer-height="7%" padding="1.2in 0.2in 0.2in 0.2in" size="Letter">

    <!-- Item Table Section -->
    <#if record.item?has_content>
      <table class="itemtable" style="width: 100%; margin-top: 0px; border: 1px solid #000;">
        <thead>
          <tr rowspan="3" style="border-bottom: 1px solid #000; border-right:1px solid #191414; border-top:1px solid black; height:50px;">
            <th colspan="2" align="center" style="border-right:1px solid #000; padding:2px;">Sl <br />No.</th>
            <th colspan="9" align="center" style="border-right:1px solid #000; padding:2px;">Particulars</th>
            <th colspan="6" align="center" style="border-right:1px solid #000;">HSN/SAC</th>
            <th colspan="3" align="center" style="border-right:1px solid #000;">Quantity</th>
            <th colspan="4" align="center" style="border-right:1px solid #000;">${record.item[0].rate@label}</th>
            <th colspan="3" align="center" style="border-right:1px solid #000;">per</th>
            <th colspan="6" align="center">${record.item[0].amount@label}</th>
          </tr>
        </thead>
        <tbody>
          <#list record.item as item>
            <tr style="height:18px;">
              <td colspan="2" line-height="150%" align="center" style="border-right:1px solid #000; padding:5px;">${item?counter}</td>
              <td colspan="9" align="left" style="border-right:1px solid #000; padding:5px;">
                <span class="itemname">${item.item}</span>
                <br />${item.description}
              </td>
              <td colspan="6" align="center" style="border-right:1px solid #000;">${item.custcol_ags_hsn_code}</td>
              <td colspan="3" align="center" style="border-right:1px solid #000;">${item.quantity}</td>
              <td colspan="4" align="center" style="border-right:1px solid #000;">${item.rate}</td>
              <td colspan="3" align="center" style="border-right:1px solid #000;"></td>
              <td colspan="6" align="right" style="padding:5px;">
                <b>${nsformat_currency(item.grossamt)}</b>
              </td>
            </tr>
          </#list>
          <!-- Empty spacer row -->
          <tr>
            <td colspan="2" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="9" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="6" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="3" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="4" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="3" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="6" align="center" style="padding:2px;"></td>
          </tr>
        </tbody>
      </table>
    </#if>

    <table style="width: 100%; margin-top: 0px; border: 1px solid #000; height:18px;">
      <tr>
        <td colspan="2" style="border-right: 1px solid #000;"></td>
        <td colspan="9" align="right" style="font-size:14px; text-align:center; padding-top:4px; border-right: 1px solid #000;"><p style="padding-right:2px;">${record.total@label}</p></td>
        <td colspan="6" align="center" style="border-right:1px solid #000; padding:2px;"></td>
        <td colspan="3" align="center" style="border-right:1px solid #000; padding:2px;"></td>
        <td colspan="4" style="font-size:14px; border-right: 1px solid #000;"></td>
        <td colspan="3" align="center" style="border-right:1px solid #000; padding:2px;"></td>
        <td colspan="6" align="right" style="font-size:13px; padding-top:4px; font-weight:bold;"><p style="padding-right:2px;">${nsformat_currency(record.total)}</p></td>
      </tr>
    </table>

   <table style="width: 100%; border-collapse: collapse; font-family: sans-serif; font-size: 12px; border: 1px solid #000; border-top: none;">

      <!-- Row 1: Amount Chargeable label + E.&O.E -->
      <tr>
        <td colspan="17" style="padding: 3px 5px;">Amount Chargeable (in words)</td>
        <td colspan="17" align="right" style="padding: 3px 5px;">E. &amp; O.E</td>
      </tr>

      <!-- Row 2: Amount in words (full width) -->
      <tr>
        <td colspan="34" style="padding: 3px 5px; font-size: 10px; font-weight: bold;">
          ${record.custbody_ags_amt_to_words_2!''}
        </td>
      </tr>
</table>
<table style="width: 100%;border-collapse: collapse; font-family: sans-serif; font-size: 12px; border: 1px solid #000;border-top: none; page-break-before: always;">
      <!-- Row 3: Tax Table (HSN/SAC, Taxable Value, IGST, Total Tax Amount) -->
     <tr>
  <td colspan="34" style="padding: 0;">

<#assign isIGST = false>
<#list record.item as item>
  <#if item.taxtotal41?has_content>
    <#assign val = item.taxtotal41?number>
    <#if (val > 0)>
      <#assign isIGST = true>
    </#if>
  </#if>
</#list>

<!-- ========================================
     STEP 2: isIGST flag ke basis pe table render karo
======================================== -->
<table style="font-size: 11px; width: 100%; border-collapse: collapse;">

  <#if isIGST>
  <!-- ===== IGST TABLE ===== -->

    <!-- Header Row 1 -->
    <tr>
      <td rowspan="2" colspan="4" align="center"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        HSN/SAC
      </td>
      <td rowspan="2" align="center"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        Taxable<br/>Value
      </td>
      <td colspan="2" align="center"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        Integrated Tax
      </td>
      <td rowspan="2" align="center"
          style="border-top:1px solid #000; border-bottom:1px solid #000;
                 padding:3px 5px;">
        Total<br/>Tax Amount
      </td>
    </tr>

    <!-- Header Row 2 -->
    <tr>
      <td align="center"
          style="border-right:1px solid #000; border-bottom:1px solid #000; padding:3px 5px;">
        Rate
      </td>
      <td align="center"
          style="border-right:1px solid #000; border-bottom:1px solid #000; padding:3px 5px;">
        Amount
      </td>
    </tr>

    <!-- Data Rows -->
    <#list record.item as item>
    <tr>
      <td colspan="4" align="left"
          style="border-right:1px solid #000; padding:3px 5px;">
        ${item.custcol_ags_hsn_code!''}
      </td>
      <td align="right"
          style="border-right:1px solid #000; padding:3px 5px;">
        ${nsformat_currency(item.amount)}
      </td>
      <td align="center"
          style="border-right:1px solid #000; padding:3px 5px;">
        ${item.taxrate1!''}
      </td>
      <td align="right"
          style="border-right:1px solid #000; padding:3px 5px;">
        ${nsformat_currency(item.taxtotal41)}
      </td>
      <td align="right" style="padding:3px 5px;">
        ${nsformat_currency(item.taxtotal41)}
      </td>
    </tr>
    </#list>

    <!-- Total Row -->
    <tr>
      <td colspan="4" align="right"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        <strong>Total</strong>
      </td>
      <td align="right"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        <strong>${nsformat_currency(record.subtotal)}</strong>
      </td>
      <td style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
      </td>
      <td align="right"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        <strong>${nsformat_currency(record.taxtotal)}</strong>
      </td>
      <td align="right"
          style="border-top:1px solid #000; border-bottom:1px solid #000; padding:3px 5px;">
        <strong>${nsformat_currency(record.taxtotal)}</strong>
      </td>
    </tr>

  <#else>
  <!-- ===== CGST + SGST TABLE ===== -->

    <!-- Header Row 1 -->
    <tr>
      <td rowspan="2" colspan="4" align="center"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        HSN/SAC
      </td>
      <td rowspan="2" align="center"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        Taxable<br/>Value
      </td>
      <td colspan="2" align="center"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        CGST
      </td>
      <td colspan="2" align="center"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        SGST
      </td>
      <td rowspan="2" align="center"
          style="border-top:1px solid #000; border-bottom:1px solid #000;
                 padding:3px 5px;">
        Total<br/>Tax Amount
      </td>
    </tr>

    <!-- Header Row 2 -->
    <tr>
      <td align="center"
          style="border-right:1px solid #000; border-bottom:1px solid #000; padding:3px 5px;">
        Rate
      </td>
      <td align="center"
          style="border-right:1px solid #000; border-bottom:1px solid #000; padding:3px 5px;">
        Amount
      </td>
      <td align="center"
          style="border-right:1px solid #000; border-bottom:1px solid #000; padding:3px 5px;">
        Rate
      </td>
      <td align="center"
          style="border-right:1px solid #000; border-bottom:1px solid #000; padding:3px 5px;">
        Amount
      </td>
    </tr>

    <!-- Data Rows -->
    <#list record.item as item>
    <tr>
      <td colspan="4" align="left"
          style="border-right:1px solid #000; padding:3px 5px;">
        ${item.custcol_ags_hsn_code!''}
      </td>
      <td align="right"
          style="border-right:1px solid #000; padding:3px 5px;">
        ${nsformat_currency(item.amount)}
      </td>
      <td align="center"
          style="border-right:1px solid #000; padding:3px 5px;">
        ${item.custcol_in_tax_rate!''}
      </td>
      <td align="right"
          style="border-right:1px solid #000; padding:3px 5px;">
        ${nsformat_currency(item.taxtotal42)}
      </td>
      <td align="center"
          style="border-right:1px solid #000; padding:3px 5px;">
        ${item.custcol_in_tax_rate!''}
      </td>
      <td align="right"
          style="border-right:1px solid #000; padding:3px 5px;">
        ${nsformat_currency(item.taxtotal43)}
      </td>
      <td align="right" style="padding:3px 5px;">
        ${nsformat_currency(item.taxtotal)}
      </td>
    </tr>
    </#list>

    <!-- Total Row -->
    <tr>
      <td colspan="4" align="right"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        <strong>Total</strong>
      </td>
      <td align="right"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        <strong>${nsformat_currency(record.subtotal)}</strong>
      </td>
      <td style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
      </td>
      <td align="right"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        <strong>${nsformat_currency(record.taxtotal42)}</strong>
      </td>
      <td style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
      </td>
      <td align="right"
          style="border-top:1px solid #000; border-right:1px solid #000;
                 border-bottom:1px solid #000; padding:3px 5px;">
        <strong>${nsformat_currency(record.taxtotal43)}</strong>
      </td>
      <td align="right"
          style="border-top:1px solid #000; border-bottom:1px solid #000; padding:3px 5px;">
        <strong>${nsformat_currency(record.taxtotal)}</strong>
      </td>
    </tr>

  </#if>

</table>
  </td>
</tr>

      <!-- Row 4: Tax Amount in words (left) | Company Bank Details + Signatory (right) -->
      <!-- Row 4: Tax Amount in words -->
<tr>
  <td colspan="34" style="padding: 5px; vertical-align: top;">
    <p style="margin: 0; padding: 0;">
      Tax Amount (in words) : &nbsp;
      <strong>${record.custbody_ags_taxamt_to_words_2!'NIL'}</strong>
    </p>
  </td>
</tr>
      <!-- PAN + Bank Details + Authorized Signatory -->
<tr>

  <!-- LEFT SIDE: PAN + Bank Details -->
  <td colspan="17" style="padding: 5px; vertical-align: top;">

    <!-- PAN -->
    <p style="margin:0 0 6px 0; font-size:10px;">
      Company's PAN/IEC Code : 
      <b>${Subsidiary.custrecord_in_permanent_account_number}</b>
    </p>

    <!-- Declaration -->
    <p style="margin:0 0 6px 0; font-size:10px; text-decoration:underline;">
      Declaration
    </p>
    <p style="margin:0 0 8px 0; font-size:10px; line-height:14px;">
      This tax invoice is issued as per the applicable provisions 
      of the GST regulations introduced in India effective from 
      July 1, 2017 onwards.
    </p>

    <!-- Bank Details -->
    <p style="margin:0 0 4px 0; font-size:10px; font-weight:bold;">
      Company's Bank Details
    </p>
    <p style="margin:0; font-size:10px; line-height:14px;">
      Bank Name: <b>${Subsidiary.custrecord_ags_bank_name!''}</b><br/>
      A/c No.: <b>${Subsidiary.custrecord_ags_account_number!''}</b><br/>
      Branch &amp; IFS Code: <b>${Subsidiary.custrecord_ags_branch_name!''} &amp; ${Subsidiary.custrecord_ags_ifsc_code!''}</b><br/>
      SWIFT Code: <b>${Subsidiary.custrecord_ags_swift_code!''}</b>
    </p>

  </td>

  <!-- RIGHT SIDE: Signatory -->
  <td colspan="17" style="border-left: 1px solid black; border-top: 1px solid black;">
    <table style="border-collapse: collapse; width: 100%;">

      <tr style="height:50px;">
        <td colspan="6"></td>
        <td align="right" colspan="11" 
            style="font-size:9pt; font-weight:bold;">
          for ${Subsidiary.legalname}
        </td>
      </tr>

      <tr>
        <td colspan="17" align="right" 
            style="font-size:9pt; text-align:right; vertical-align:bottom;">
          Authorized Signatory
        </td>
      </tr>

    </table>
  </td>

</tr>

    </table>
  </body>
</pdf>