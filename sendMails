
// functions for sending mails in google sheets.
function getPDF(req_num) {
  var url = "https://holidale.com/preview/" + req_num.toString(10) + ".pdf?locale=en"; 
  var params = {
    method: "get",
    headers: {"Authorization": "Bearer " + ScriptApp.getOAuthToken()}
  };
  var response = UrlFetchApp.fetch(url, params);
  var text = response.getResponseCode();
  if (text == '200'){
    var blob = response.getBlob().setName("Your requested.pdf");
    return blob;
  }else{
    Logger.log('Error');
    return null;
  } 
}

function sendMail() {
  var data = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet().getDataRange().getValues();
  if (data.length > 1){
     for (var i = 1;  i < data.length; i++){// start from the row 1
        var username = data[i][0];
        var email = data[i][1];
        var address = data[i][2];
        var numberOfInterest = data[i][3];
      
        //get data from the target
        var pdfFile = getPDF(parseInt(numberOfInterest));
       var content = "<p>Hi " + username + "</p><p>Here are some information about House" + numberOfInterest +  " you are interested in: </p> <p>Address:"+ address + "</p> <p>Best regards,<br>Oliver</p>";
        MailApp.sendEmail({
            to: email,
            subject: "your Email",
            htmlBody: content,
            attachments:[pdfFile] // Modified
        })
    }
  }
  else{
    Logger.log('Error! The table is empty!');
  }
}

