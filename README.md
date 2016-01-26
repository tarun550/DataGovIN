# Data.gov.in API sample
A tutorial demonstrating the usage of data.gov.in (The documentation on the website not being elobraote enough)

The data.gov.in APIs have a very simple format. The need a secret-key and an identifier for the data set.
After that the request paramters mimic the SQL commands. So if you know SQL, this should be very easy.

Lets start with the resource id. If I need to search the company master record of Uttar Pradesh(upto 2015), I have a predefined resource_id as "f8547c08-a7bf-4e85-b179-c57b5bd135a8". This needs to be one of the URL paramters.
If you need the specific resource_id please visit [https://data.gov.in/catalogs]

Now lets get a secret key. You can easily get one after registering here [https://auth.mygov.in/user/register?destination=oauth2/register/datagovindia]


So now lets get ready to write our own URL for the API.
Please read the API documentation given in any of the catalogs. Then you can co-relate better with what is coming next

Lets first start with what all fields are available to me, for the data API.
I am going to set "limit=0", so that I donot get unnecessary data on my request.

Do a call to https://data.gov.in/api/datastore/resource.json?resource_id=f8547c08-a7bf-4e85-b179-c57b5bd135a8&api-key=API_KEY&limit=0

The response should be similar to

	"help": "Search a datastore table. :param resource_id: id or alias of the data that is going to be selected."
	
	"success": false
	
	"count": 0
	
	"fields": {
		  "id": {
			    "type": "serial"
			    "size": "normal"
			    "unsigned": true
			    "not null": true
			    "description": ""
		  }-
		  
		  "timestamp": {
			    "type": "timestamp"
			    "size": "normal"
			    "not null": true
			    "default": "CURRENT_TIMESTAMP"
			    "description": ""
		  }-
		  
		  "CORPORATEIDENTIFICATIONNUMBER": {
			    "type": "varchar"
			    "size": "normal"
			    "length": "21"
			    "not null": false
			    "description": ""
		  }-
		  
		  "DATEOFREGISTRATION": {
			    "type": "varchar"
			    "size": "normal"
			    "length": "10"
			    "not null": false
			    "description": ""
		  }-
	
...... and so on

These are the "fields" which we can use in our query. Now we can use these fields to create a SQL like query.

TO make things simple, lets say I wish to find "CORPORATEIDENTIFICATIONNUMBER" of all companies that are "Private".
My query will be
https://data.gov.in/api/datastore/resource.json?resource_id=f8547c08-a7bf-4e85-b179-c57b5bd135a8&api-key=API_KEY&limit=10&filters[COMPANYCLASS]=Private

We can perform operations like JOIN, SORT, LIMIT AND OFFSET to make this API more interactive.

From what I felt was that I cannot use operators other than "=". So its difficult to get records where a condition is negative.

Please leave your comments incase you need more help.
  
  
  
  

