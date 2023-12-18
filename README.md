<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Salary Slip Generator</title>
    <style>
        body {
            padding: 20px;
            height: 2480px;
            width: 3508;
            top:90px;
            border: 2px solid #000;
            outline: 5px solid white;
            margin-top: 30px;
            margin-bottom: 30px;
        }

        table {
            border-collapse: collapse;
            width:300;
            margin-top: 20px;
        }

        th, td {
            border: 1px solid black;
            padding: 8px;
            text-align: left;
        }

        th {
            background-color: #f2f2f2;
        }
        table, th, td {
            border: 1px solid black;
        }
           input[type="text"] {
            padding: 5px;
            width: 100%;
        }

        button {
            padding: 8px 16px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }

    </style>
</head>
<body>
    <h1>PERFORMA INVOICE Generator</h1>

    <label for="Shiptocompany">Enter Consignee (Ship to) Company Name:</label>
    <input type="text" id="Shiptocompany"><br>

    <label for="Shiptoadress">Enter Consignee (Ship to) Company Address:</label>
    <input type="text" id="Shiptoadress"><br>

    <label for="Shiptostate">Enter Consignee (Ship to) Company State:</label>
    <input type="text" id="Shiptostate"><br>

    <label for="uan">Enter Company State Code:</label>
    <input type="text" id="uan"><br>

    <label for="GST">Enter Company GSTIN/UIN:</label>
    <input type="text" id="GST"><br>

    <label for="Shiptocompany1">Buyer (Bill to) Company Name:</label>
    <input type="text" id="Shiptocompany1"><br>

    <label for="Shiptoadress1">Enter Buyer (Bill to) Company Address:</label>
    <input type="text" id="Shiptoadress1"><br>

    <label for="Shiptostate1">Enter Buyer (Bill to) Company State:</label>
    <input type="text" id="Shiptostate1"><br>

    <label for="uan1">Enter Buyer (Bill to) State Code:</label>
    <input type="text" id="uan1"><br>

    <button onclick="generatePerformaInvoice()">Generate</button>
    <div>
      
        <label for="sl_no">Sl. No.:</label>
        <input type="text" id="sl_no">
        <label for="description">Description:</label>
        <input type="text" id="description">
        <label for="quantity">Quantity:</label>
        <input type="text" id="quantity">
          <label for="HSN">HSN/SAC:</label>
        <input type="text" id="HSN">
        <label for="Ratel">Rate(Incl. of Tax):</label>
        <input type="text" id="Ratel">
         <label for="Rate">Rate :</label>
        <input type="text" id="Rate">
         <label for="Per">Per :</label>
        <input type="text" id="Per">
         <label for="Disc">Disc. % :</label>
        <input type="text" id="Disc">
        <label for="choices">Select GST:</label>
  <select id="choices" name="choices">
    <option value="CGST&SGST">CGST&SGST</option>
    <option value="IGST">IGST</option>
  </select>
  <label for="taxRate">Select Tax Rate:</label>
  <select id="taxRate" name="taxRate">
    <option value="0.18">18%</option>
    <option value="0.28">28%</option>
    <option value="0.12">12%</option>
    <option value="0.05">5%</option>
  </select>
   
  

        
        
         
        <button onclick="addRow()">Add Row</button>
    </div>

    <div id="performaInvoice"></div>

    <script>
    
        function generatePerformaInvoice() {
            const Shiptocompany = document.getElementById("Shiptocompany").value;
            const Shiptoadress = document.getElementById("Shiptoadress").value;
            const Shiptostate = document.getElementById("Shiptostate").value;
            const uan = document.getElementById("uan").value;
            const GST = document.getElementById("GST").value;
            const Shiptocompany1 = document.getElementById("Shiptocompany1").value;
            const Shiptoadress1 = document.getElementById("Shiptoadress1").value;
            const Shiptostate1 = document.getElementById("Shiptostate1").value;
            const uan1 = document.getElementById("uan1").value;

            const MyaddressTable = `
                <table>
                    <tr>
                        <th><b>Mandhira Realty Ventures Private Limited<br>#5/4/6, 2nd main, 11th cross , Hoysala Nagar, Herohalli, <br>Bangalore North, Bangalore 560091.<br>State Name : Karnataka , Code :29<br>
                        GSTIN/UIN: ${GST}<br>
                        Email :director@mandhiravetures.com<br>
                        Mobile No: +917337880790 <br></th>
                    </tr>
                </table>
            `;
            const MyaddressTable2 = `
                <table>
                    <tr>
                        <th>Consignee (Ship to) :${Shiptocompany}<br>${Shiptoadress}<br>State Name:${Shiptostate}<br>State Code: ${uan}<br>GSTIN/UIN: ${GST}</th>
                    </tr>
                </table>
            `;
            const BuyeraddressTable2 = `
                <table>
                    <tr>
                        <th>Consignee (Ship to) :${Shiptocompany1}<br>${Shiptoadress1}<br>State Name:${Shiptostate1}<br>State Code: ${uan1}<br>GSTIN/UIN: ${GST}</th>
                    </tr>
                </table>
            `;

const Bankdetails=`<table>
<tr>
<th>Company Bank Details</th>
<tr>
<tr>
<td>Bank Name	: HDFC BANK<br>A/c No.	:  50200084872542<br>Branch  : SadashivaNagar 15th Main, Bangloore <br>IFS Code: HDFC0004823<br>Company's PAN	:AARCM3428J  </td>
</tr>
</table>`;
const signature=`<table>
<tr>
<th>Mandhira Realty Ventures Private Limited</th>
<tr>
<tr>
<td>             <br>Authorised Signature</td>
</tr>
</table>
<p><b>Declaration</b><br>
Goods once sold cannot be taken back or exchanged.</p>
`;
            const performaInvoice = `
                <h2>PERFORMA INVOICE</h2>
                ${MyaddressTable}
                ${MyaddressTable2}
                ${BuyeraddressTable2}
                 <table id="data_table">
        <thead>
            <tr>
                <th>Sl. No.</th>
                <th>Description</th>
                <th>Quantity</th>
                <th>HSN</th>
                <th>Rate(Incl. of Tax)</th>
                <th>Rate</th>
                <th>Per</th>
                <th>Disc. %</th>
                <th>Ammount</th>
            </tr>
        </thead>
        <tbody>
            <!-- Table content will be added dynamically -->
        </tbody>
    </table>

    <div id="total_quantity"></div>
    <div id="HSN_data"></div>
    <div id="Tax_value"></div>
    <div id ="Selected_gst"></div>
    <div id="Tax_Rates"></div>
    <div id="GST_Ammount"></div>
    <div id="Tota_incl"></div>
      <div id="text_result"></div>
    <div id="text_result2"></div>
    ${Bankdetails}
    ${signature}
    
            `;

            document.getElementById("performaInvoice").innerHTML = performaInvoice;
        }
        function addRow() {
            var slNo = document.getElementById("sl_no").value;
            var description = document.getElementById("description").value;
            var quantity = document.getElementById("quantity").value;
            var HSN= document.getElementById("HSN").value;
            var Ratel=document.getElementById("Ratel").value;
            var Rate=document.getElementById("Rate").value;
            var Per=document.getElementById("Per").value;
            var Disc=document.getElementById("Disc").value;
             var choices = document.getElementById("choices").value;
             var taxRate=document.getElementById("taxRate").value;
            var Ammount=quantity*Rate;

            var table = document.getElementById("data_table").getElementsByTagName('tbody')[0];
            var newRow = table.insertRow(table.rows.length);

            var cell1 = newRow.insertCell(0);
            var cell2 = newRow.insertCell(1);
            var cell3 = newRow.insertCell(2);
            var cell4 = newRow.insertCell(3);
            var cell5 = newRow.insertCell(4);
            var cell6 =newRow.insertCell(5);
            var cell7=newRow.insertCell(6);
            var cell8=newRow.insertCell(7);
            var cell9=newRow.insertCell(8);
            

            cell1.innerHTML = slNo;
            cell2.innerHTML = description;
            cell3.innerHTML = quantity;
            cell4.innerHTML = HSN;
            cell5.innerHTML=Ratel;
            cell6.innerHTML=Rate;
            cell7.innerHTML=Per;
            cell8.innerHTML=Disc;
            cell9.innerHTML=Ammount;

            // Reset input fields after adding row
            document.getElementById("sl_no").value = "";
            document.getElementById("description").value = "";
            document.getElementById("quantity").value = "";
            document.getElementById("HSN").value="";
            document.getElementById("Ratel").value="";
            document.getElementById("Rate").value=" ";
            document.getElementById("Disc").value=" ";
            document.getElementById("Per").value=" ";
            document.getElementById("choices").value=" ";
            document.getElementById("taxRate").value=" ";
     
            updateTotalQuantity(taxRate,choices);
            document.getElementById("HSN_data").innerHTML = "HSN/SAC: " + HSN;
              document.getElementById("Selected_gst").innerHTML = "GST Applicable: " + choices;
            document.getElementById("Tax_Rates").innerHTML="GST Tax Rate: "+taxRate*100+"%";
              
             
        }
        function updateTotalQuantity(taxRate,choices) {
            var table = document.getElementById("data_table").getElementsByTagName('tbody')[0];
            var rows = table.getElementsByTagName('tr');
            var totalQuantity = 0;

            for (var i = 0; i < rows.length; i++) {
                var quantity = parseInt(rows[i].getElementsByTagName('td')[8].innerHTML, 10);
                if (!isNaN(quantity)) {
                    totalQuantity += quantity;
                }
            }

           document.getElementById("total_quantity").innerHTML = "Total Ammount: " + totalQuantity;
           var text= numberToText(totalQuantity);

         document.getElementById("Tax_value").innerHTML = "Taxable Value : " + totalQuantity;
        var taxcaluclated=totalQuantity*taxRate;     
        if(choices=="IGST")
        document.getElementById("GST_Ammount").innerHTML = "GST Ammount : " + taxcaluclated.toFixed(2);
        else
document.getElementById("GST_Ammount").innerHTML = "GST Ammount CGST "+((taxRate/2)*100)+"%: " + (taxcaluclated.toFixed(2)/2) + "<br> GST_Ammount SGST "+((taxRate/2)*100)+"%: " + (taxcaluclated.toFixed(2)/2);
var Tt_incl=totalQuantity+(taxRate*totalQuantity);
Tt_incl=Math.ceil(Tt_incl);
document.getElementById("Tota_incl").innerHTML = "Total  Ammount inclusion of GST is  : " + Tt_incl.toFixed(0);
       var text2=numberToText(Tt_incl);
                      document.getElementById("text_result").innerHTML = "<strong>Ammount in words: " + text+".</strong>";
                                     document.getElementById("text_result2").innerHTML = "<strong>Total Ammount inclusion of GST in words: " + text2+".</strong>";
       }
        function numberToText(number) {
    var units = ['Zero', 'One', 'Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine'];
    var teens = ['Eleven', 'Twelve', 'Thirteen', 'Fourteen', 'Fifteen', 'Sixteen', 'Seventeen', 'Eighteen', 'Nineteen'];
    var tens = ['', '', 'Twenty', 'Thirty', 'Forty', 'Fifty', 'Sixty', 'Seventy', 'Eighty', 'Ninety'];

    function convertLessThanOneThousand(n) {
        if (n < 10) return units[n];
        if (n < 20) return teens[n - 11];
        if (n < 100) return tens[Math.floor(n / 10)] + (n % 10 !== 0 ? ' ' + units[n % 10] : '');
        if (n < 1000) return units[Math.floor(n / 100)] + ' Hundred' + (n % 100 !== 0 ? ' and ' + convertLessThanOneThousand(n % 100) : '');
    }

    if (number === 0) return units[0];
    if (number < 0) return 'Minus ' + numberToText(-number);

    var chunks = [];
    while (number > 0) {
        chunks.push(number % 1000);
        number = Math.floor(number / 1000);
    }

    var chunkCount = chunks.length;

    if (chunkCount > 1 && chunks[0] === 0) {
        chunks.shift();
        chunkCount--;
    }

    var words = [];
    for (var i = 0; i < chunkCount; i++) {
        var chunk = chunks[i];
        if (chunk !== 0) {
            words.push(convertLessThanOneThousand(chunk));
            if (i !== chunkCount - 1) {
                words.push(chunk !== 1 ? ' Thousand' : ' Thousand');
            }
        }
    }

    return words.reverse().join(' ');
}
    </script>
</body>
</html>
