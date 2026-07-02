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
    <macrolist>
      <macro id="nlheader">
        <table style="width: 100%; border-collapse: collapse; margin-top: 100px;">
          <tr>
            <td align="center" style="text-align: center; font-size: 16px; font-weight: bold; padding-bottom: 15px;">
              Tax Invoice
            </td>
          </tr>
          <#if record.custbody_in_gst_lut_bond_number?has_content>
          <tr>
            <td align="center" style="text-align: center; font-size: 10px; padding-bottom: 10px;">
              (SUPPLY MEANT FOR EXPORT/SUPPLY TO SEZ UNIT OR SEZ DEVELOPER FOR AUTHORISED OPERATIONS UNDER BOND OR LETTER OF UNDERTAKING WITHOUT PAYMENT OF IGST)
            </td>
          </tr>
          </#if>
        </table>

        <table style="width: 100%; border-collapse: collapse;">
          <tr>
            <td style="width: 55%; vertical-align: bottom; font-size: 11px; line-height: 16px; padding-bottom: 8px;">
              IRN : <b>${record.custbody_in_ei_irn!''}</b><br />
              Ack No. : <b>${record.custbody_in_ei_ackno!''}</b><br />
              Ack Date : 
              <#assign ackDateStr = custbody_in_ei_ackdt!''>
              <#if ackDateStr?has_content && (ackDateStr?length == 19)>
                <b>${ackDateStr?datetime("yyyy-MM-dd HH:mm:ss")?string("yyyy-MM-dd HH:mm:ss")}</b>
              <#else>
                <b>${ackDateStr}</b>
              </#if>
            </td>

            <td style="width: 45%; vertical-align: bottom; text-align: right; align: right; padding-bottom: 8px;">
              <table align="right" style="border-collapse: collapse;">
                <tr>
                  <#if record.custbody_in_ei_irn?has_content>
                    <td style="padding-right: 15px; vertical-align: bottom;">
                      <barcode codetype="qrcode" height="80px" width="80px" showtext="false" value="${record.custbody_ageinv_signedqrcode!''}"/>
                    </td>
                  <#elseif record.custbody_in_ei_irn?has_content>
                    <td style="padding-right: 15px; vertical-align: bottom;">
                      <barcode codetype="qrcode" height="80px" width="80px" showtext="false" value="${record.custbody_in_ei_irn!''}"/>
                    </td>
                  </#if>

                  <#if companyInformation.logoUrl?has_content>
                    <td style="vertical-align: bottom;">
                      <img src="${companyInformation.logoUrl}" style="height: 55px; width: 110px;"/>
                    </td>
                  </#if>
                </tr>
              </table>
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
        <table class="submain">
          <tr>
            <td style="border-right: 1px solid #000;">
              <table class="leftsection" style="height:100%; width:100%; margin-right:-2px; margin-left:-2px;">
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
                <tr style="height: 185px;">
                  <td style="padding-top: 5px;">
                    <p style="padding-left:5px; padding-top:2px; line-height:16px; font-size:10px;">
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

            <td style="width: 50%; padding: 0px; vertical-align: top;">
              <table class="rightsection">
                <tr style="border-bottom: 1px solid #000; height: 28px;">
                  <td style="border-right:1px solid #000;">
                    <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
                      Invoice No.<br/><b>${record.custbody_ags_invnumber}</b>
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
                      ${record.terms?has_content?then(record.terms,'<b>Due on receipt</b>')}
                    </p>
                  </td>
                </tr>
                <tr style="border-bottom: 1px solid #000; height: 38px;">
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
                <tr style="border-bottom: 1px solid #000; height: 38px;">
                  <td colspan="2">
                    <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
                      Buyer's Order No. &amp; Date <br/><b>${record.tranid} &amp; ${record.trandate}</b>
                    </p>
                  </td>
                  <!-- <td>
                    <p style="font-size:10px; padding: 2px 3px; line-height:14px;">
                      Dated<br/><b></b>
                    </p>
                  </td> -->
                </tr>
                <tr style="border-bottom: 1px solid #000; height: 38px;">
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
        <table style="width: 100%; border-collapse: collapse;">
          <tr>
            <td align="center" style="text-align: center; vertical-align: middle;">
              <p style="font-size: 8.5pt; font-weight: bold; color: #333333; margin: 0; padding: 2px 0; text-transform: uppercase; letter-spacing: 0.5px;">SUBJECT TO MUMBAI JURISDICTION</p>
              <p style="font-size: 8pt; color: #555555; margin: 0; padding: 2px 0;">This is a computer generated invoice.</p>
            </td>
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
      table { table-layout: fixed; }
      th { font-weight: bold; vertical-align: middle; padding: 5px 6px 3px; color: #333333; }
      body { font-size: 10px; }
      b { font-weight: bold; color: #333333; }
      table.header td { padding: 0px; }
      table.footer td { padding: 0px; }
      table.itemtable th { padding-bottom: 10px; padding-top: 10px; }
      table.body td { padding-top: 2px; }
      table.total { page-break-inside: avoid; }
      tr.totalrow { line-height: 200%; }
      td.addressheader { padding-top: 6px; padding-bottom: 2px; }
      td.address { padding-top: 0px; }
      td.totalboxbot { font-weight: bold; }
      span.title { font-size: 16pt; font-weight: bold; font-family: sans-serif; }
      span.number { font-size: 16pt; }
      span.itemname { font-weight: bold; line-height: 150%; }
      hr { width: 100%; height: 1px; }
      .left-section { width: 50%; font-size: 14px; }
      .right-section { width: 50%; }
      .bold { font-weight: bold; }
      .section-title { margin: 0; font-size: 1.1em; text-decoration: underline; }
      .data-table { width: 100%; border-collapse: collapse; margin-top: 10px; }
      .data-table td { border: 1px solid black; padding: 5px; text-align: left; }
      .main { width: 100%; margin-top: 10px; overflow:hidden; border-collapse: collapse; line-height:10px; }
      .main td { width: 100%; padding: 0; }
      .submain { width: 100%; border: 1px solid #000; border-bottom:1px; border-collapse: collapse; font-size: 10px; }
      .submain td { width: 50%; vertical-align: top; }
      .leftsection { width: 100%; border-collapse: collapse; margin-top: 2px; font-family: sans-serif; }
      .leftsection tr { margin-top: 2px; font-size: 14px; font-family: sans-serif; }
      .rightsection { width: 100%; border-collapse: collapse; }
      .rightsection tr { font-family: sans-serif; height: 2%; }
      .rightsection td { padding: 2px; font-size: 12px; padding-bottom: 2px; }
      .itemtable { overflow:hidden; width:100%; height:300px; }
      #taxtable { width: 100%; margin-top: 0; border-collapse: collapse; }
      #taxtable td { border: 1px solid black; }
    </style>
  </head>

  <body header="nlheader" header-height="5.8in" footer="nlfooter" footer-height="0.6in" padding="0.2in 0.2in 0.2in 0.2in" size="Letter">
    <#if record.item?has_content>
      <table class="itemtable" style="width: 100%; margin-top:0px; border-left: 1px solid #000; border-right: 1px solid #000; border-bottom:1px solid #000;">
        <thead>
          <tr rowspan="3" style="border-bottom: 1px solid #000; border-right:1px solid #191414; border-top:1px solid black; height:50px; ">
            <th colspan="2" align="center" style="border-right:1px solid #000; padding:2px;">Sl <br />No.</th>
            <th colspan="6" align="center" style="border-right:1px solid #000; padding:2px;">Particulars</th>
            <th colspan="4" align="center" style="border-right:1px solid #000;">HSN/SAC</th>
            <th colspan="2" align="center" style="border-right:1px solid #000;">Qty</th>
            <th colspan="4" align="center" style="border-right:1px solid #000;">${record.item[0].rate@label}</th>
            <th colspan="5" align="center" style="border-right:1px solid #000;">Taxable Amount</th>
            <th colspan="2" align="center" style="border-right:1px solid #000;">Tax <br /> Rate</th>
            <th colspan="4" align="center" style="border-right:1px solid #000;">Tax Amount</th>
            <th colspan="5" align="center">${record.item[0].amount@label}</th>
          </tr>
        </thead>
        <tbody>
          <#list record.item as item>
            <tr style="height:18px;">
              <td colspan="2" line-height="150%" align="center" style="border-right:1px solid #000; padding:5px;">${item?counter}</td>
              <td colspan="6" align="left" style="border-right:1px solid #000; padding:5px;">
                <span class="itemname">${item.item}</span>
                <br />${item.description}
              </td>
              <!-- <#assign cleanAmount = (item.amount!'0')?replace('[^0-9.]', '', 'r') />
              <#assign taxableAmount = cleanAmount?number />
              <#assign total_tax = taxableAmount * 0.18 />
              <#assign itemTotal = taxableAmount + total_tax /> -->
              <#assign rawRate = item.taxrate1!'' />
<#assign cleanRate = rawRate?replace('[^0-9.]', '', 'r') />
<#if cleanRate?has_content>
  <#assign taxRate = cleanRate?number />
<#else>
  <#assign taxRate = 0 />
</#if>

<#assign total_tax = taxableAmount * (taxRate/100) />
<#assign itemTotal = taxableAmount + total_tax />
              <td colspan="4" align="center" style="border-right:1px solid #000;">${item.custcol_ags_hsn_code}</td>
              <td colspan="2" align="center" style="border-right:1px solid #000;">${item.quantity}</td>
              <td colspan="4" align="center" style="border-right:1px solid #000;">${item.rate}</td>
              <td colspan="5" align="center" style="border-right:1px solid #000;">${nsformat_currency(item.amount)}</td>
              <td colspan="2" align="center" style="border-right:1px solid #000;">${item.taxrate1}</td>
              <td colspan="4" align="center" style="border-right:1px solid #000;">${nsformat_currency(total_tax)}</td>
              <td colspan="5" align="right" style="padding:5px;">
                <b>${nsformat_currency(itemTotal)}</b>
              </td>
            </tr>
          </#list>
          <tr>
            <td colspan="2" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="6" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="4" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="2" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="4" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="5" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="2" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="4" align="center" style="border-right:1px solid #000; padding:2px;"></td>
            <td colspan="5" align="center" style="padding:2px;"></td>
          </tr>
        </tbody>
      </table>
    </#if>

    <table style="width: 100%; margin-top: 0px; border: 1px solid #000; border-top:none; height:18px;">
      <tr>
        <td colspan="2" style="border-right: 1px solid #000;"></td>
        <td colspan="6" align="right" style="font-size:14px; text-align:center; padding-top:4px; border-right: 1px solid #000;"><p style="padding-right:2px;">${record.total@label}</p></td>
        <td colspan="4" align="center" style="border-right:1px solid #000; padding:2px;"></td>
        <td colspan="2" align="center" style="border-right:1px solid #000; padding:2px;"></td>
        <td colspan="4" style="font-size:14px; border-right: 1px solid #000;"></td>
        <td colspan="5" align="center" style="border-right:1px solid #000; padding:2px;"></td>
        <td colspan="2" align="center" style="border-right:1px solid #000; padding:2px;"></td>
        <td colspan="4" align="center" style="border-right:1px solid #000; padding:2px;"></td>
        <td colspan="5" align="right" style="font-size:13px; padding-top:4px; font-weight:bold;"><p style="padding-right:2px;">${nsformat_currency(record.total)}</p></td>
      </tr>
    </table>

    <table style="width: 100%; border-collapse: collapse; font-family: sans-serif; font-size: 12px; border: 1px solid #000; border-top: none;">
      <tr>
        <td colspan="17" style="padding: 3px 5px;">Amount Chargeable (in words)</td>
        <td colspan="17" align="right" style="padding: 3px 5px;">E. &amp; O.E</td>
      </tr>
      <tr>
        <td colspan="34" style="padding: 3px 5px; font-size: 10px; font-weight: bold;">
          ${record.custbody_ags_amt_to_words_2!''}
        </td>
      </tr>
    </table>

    <table style="width: 100%; border-collapse: collapse; font-family: sans-serif; font-size: 12px; border: 1px solid black; page-break-before: always;">
      <tr>
        <td colspan="34" style="padding: 0;">
          <table style="font-size: 11px; width: 100%; border-collapse: collapse;">
            <thead>
              <tr style="background-color: #f5f5f5;">
                <th rowspan="2" colspan="14" align="center" style="border-right: 1px solid black; border-bottom: 1px solid black; padding: 5px;">Taxable<br/>Value</th>
                <th colspan="10" align="center" style="border-right: 1px solid black; border-bottom: 1px solid black; padding: 5px;">Integrated Tax</th>
                <th rowspan="2" colspan="10" align="center" style="border-bottom: 1px solid black; padding: 5px;">Total<br/>Tax Amount</th>
              </tr>
              <tr style="background-color: #f5f5f5;">
                <th colspan="4" align="center" style="border-right: 1px solid black; border-bottom: 1px solid black; padding: 5px;">Rate</th>
                <th colspan="6" align="center" style="border-right: 1px solid black; border-bottom: 1px solid black; padding: 5px;">Amount</th>
              </tr>
            </thead>
            <tbody>
              <#list record.item as item>
                <tr>
                  <td align="right" colspan="14" style="border-right: 1px solid #000; border-bottom: 1px solid black; padding: 4px 5px;">${nsformat_currency(item.amount)}</td>
                  <td align="center" colspan="4" style="border-right: 1px solid #000; border-bottom: 1px solid black; padding: 4px 5px;">${item.taxrate1!''}</td>
                  <td align="right" colspan="6" style="border-right: 1px solid #000; border-bottom: 1px solid black; padding: 4px 5px;">${nsformat_currency(item.taxtotal41)}</td>
                  <td align="right" colspan="10" style="border-bottom: 1px solid #000; padding: 4px 5px;">${nsformat_currency(item.taxtotal41)}</td>
                </tr>
              </#list>
              <tr style="font-weight: bold; background-color: #f5f5f5; border-bottom:1px solid #000;">
                <td colspan="14" align="right" style="border-right: 1px solid #000; padding: 5px;">Total:<strong>${nsformat_currency(record.subtotal)}</strong></td>
                <td align="right" colspan="4" style="border-right: 1px solid #000; padding: 5px;"></td>
                <td colspan="6" style="border-right: 1px solid #000; padding: 5px;"></td>
                <td align="right" colspan="10" style="padding: 5px;"><strong>${nsformat_currency(record.taxtotal)}</strong></td>
              </tr>
            </tbody>
          </table>
        </td>
      </tr>
  <tr>
    <td colspan="17" width="60%">
      <strong>Tax Amount (in words)</strong><br/>
      ${record.custbody_ags_amount_word}
    </td>
    <td colspan="17" align="right" style="border-left:none;">
      <em>(This amount is exclusive of all taxes)</em>
    </td>
  </tr>
 
  <!-- Signatory row -->
  <tr>
    <td colspan="17" style="border-top:none;"><p style="margin:50px 0 6px 0; font-size:10px;">
      
    Company's PAN/IEC Code : <b>${Subsidiary.custrecord_in_permanent_account_number}</b>
  </p>
  <p style="margin:0 0 6px 0; font-size:10px; text-decoration:underline;">Declaration</p>
  <p style="margin:0 0 8px 0; font-size:10px; line-height:14px;">
    This tax invoice is issued as per the applicable provisions of the GST regulations introduced in India effective from July 1, 2017 onwards.
  </p></td>
    <td colspan="17" align="left" style="border-left:none;">
      <table width="100%" style="margin:-2px;">
        <tr>
          <td colspan="17">
      <p style="margin:0 0 4px 0; font-size:10px; font-weight:bold;">Company's Bank Details</p>
        <p style="margin:0; font-size:10px; line-height:14px;">
          Bank Name: <b>${Subsidiary.custrecord_ags_bank_name!''}</b><br/>
          A/c No.: <b>${Subsidiary.custrecord_ags_account_number!''}</b><br/>
          Branch &amp; IFS Code: <b>${Subsidiary.custrecord_ags_branch_name!''} &amp; ${Subsidiary.custrecord_ags_ifsc_code!''}</b><br/>
          SWIFT Code: <b>${Subsidiary.custrecord_ags_swift_code!''}</b>
        </p></td></tr>
        <tr><td colspan="17" align="right" style="max-width:100%; border-left:1px solid black; border-top:1px solid black;" >
      <br/><br/><br/><br/>
          Authorised Signatory
        
        </td></tr>
        </table>
    </td>
  </tr>
    </table>
  </body>
</pdf>