# ajax-protected-OdataAPI

Read password protected odata API using jquery.

### beforeSend
Use beforeSend to set authorization (user name and password) for the API.
Refer odata.html for complete sample code.

```sh
$.ajax({
    type: 'GET',
    // TODO: Your URL will be different to the one below.
    url: "https://api.businesscentral.dynamics.com/v2.0/privatekey/id/ODataV4/Company('companyid')/ItemLedgerEntries",
    dataType: 'json',
    // As CORS is used, this must be set to true
    crossDomain: false,
    // Basic authentication is set in the header, enter appropriate user name and password for your environment.
    // The xhr (XMLHttpRequest) function below sends authorization details to the server.
    // This line creates a hash of the user name and password:
    // window.btoa(unescape(encodeURIComponent("[USERNAME]" + ':' + "[PASSWORD]")))
    beforeSend: function (xhr) {
        xhr.setRequestHeader('Authorization', 'Basic ' + window.btoa(unescape(encodeURIComponent("<username>" + ':' + "<password>"))));
        xhr.setRequestHeader("Content-Type", "application/json; charset=UTF-8");
    },
    // On success, we write a 'success' message to the console and stringify the returned JSON to display,
    // for example, in the <div id="t1"><div> tag on a web page
    success: function (json_data) {
        console.log('success');
        $("#apiResponse").html(JSON.stringify(json_data));
    },
    // In case of error, show an alert
    error: function () {
        alert('Failed!');
    }
})
```
