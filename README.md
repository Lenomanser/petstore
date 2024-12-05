# Test Task, Vasylenko Elena

Test cases for endpoint {{host}}//pet/{{petId}}  
https://petstore.swagger.io/#/pet/updatePetWithForm

Some test cases include assumptions or comments due to missing requirements in the provided documentation!!!

---

### Test Case № 1:
**Title:** Successful update of the pet's name  

**Description:** Verify that the endpoint correctly replaces the value of the pet's 'name' field with the value ​​passed in the request, leaving other fields of the object unchanged.  

**Preconditions:**  
1) The pet's initial data in the database is as follows  
   id = 123,  
   name = "Mur",  
   status = "available"  

**Steps:**  
1) Send a POST request to {{host}}//pet/123 with parameters:  
   name = "Updated name"  

**Expected Result:**  
1) Status code of the response: 200 OK.  
2) The name field of the pet with ID 123 is updated in the database to "Updated name".  
3) Other fields of the pet remain unchanged.  

---

### Test Case № 2:
**Title:** Successful update of the pet's status  

**Description:** Verify that the endpoint correctly replaces the value of the pet's status field with the value ​​passed in the request, leaving other fields of the object unchanged.  

**Preconditions:**  
1) The pet's initial data in the database is as follows  
   id = 123,  
   name = "Mur",  
   status = "available"  

**Steps:**  
1) Send a POST request to {{host}}//pet/123 with the following parameters:  
   status = "Sold"  

**Expected Result:**  
1) Status code of the response: 200 OK.  
2) The "status" field of the pet with ID 123 is updated in the database to "Sold".  
3) Other fields of the pet remain unchanged.  

---

### Test Case № 3:
**Title:** Update both the pet's name and status in a single request.  

**Description:** Verify that the endpoint correctly replaces two fields at once: name and status of the pet leaving other fields unchanged.  

**Preconditions:**  
1) The pet's initial data in the database is as follows  
   id = 123,  
   name = "Mur",  
   status = "available"  

**Steps:**  
1) Send a POST request to {{host}}//pet/123 with the following parameters:  
   name = "Updated name",  
   status = "Sold"  

**Expected Result:**  
1) Status code of the response: 200 OK.  
2) The name field of the pet with ID 123 is updated in the database to "Updated name".  
3) The status field of the pet with ID 123 is updated to "Sold".  
4) Other fields of the pet remain unchanged.  

---

### Test Case № 4:
**Title:** Update the pet with an invalid status value (Negative case)  

*(An invalid status is a status that is not on the list of acceptable statuses for a pet)*  

**Description:** Verify that the server returns an error when trying to update the pet's status with an invalid value.  

**Preconditions:**  
1) The pet's initial data in the database is as follows  
   id = 123,  
   name = "Mur",  
   status = "available"  

**Steps:**  
1) Send a POST request to {{host}}//pet/123 with the following parameters:  
   status = "invalid_status"  

**Expected Result:**  
1) Status code of the response: 400 Bad Request.  
2) The status field of the pet is "available" in the database.  
3) The response body contains an error message, such as "Invalid status value".  

---

### Test Case № 5:
**Title:** Updating the name field to a value that is outside the allowed length  

*(Since there are no clear requirements in the Swagger documentation, this test assumes a maximum length of 15 characters for the 'name' field as an example)*  

**Description:** Verify that the Server will return an error when trying to update the name field to a value whose length is greater than the maximum allowed.  

**Preconditions:**  
1) The pet's initial data in the database is as follows  
   id = 123,  
   name = "Mur",  
   status = "available"  

**Steps:**  
1) Send a POST request to {{host}}//pet/123 with the following parameters:  
   name = "Verylongsentence"  

**Expected Result:**  
1) Status code of the response: 400.  
2) The response body contains information about the error, such as:  
   `"The name field exceeds the allowed maximum length."`  

**Comment:** The requirements for this test case should be clarified, as the exact field length limit and error format are not specified in the documentation.  

---

### Test Case № 6:
**Title:** Update a non-existent pet (Negative case)  


**Description:** Verify that the server returns an error when attempting to update a pet that does not exist in the database.  

**Preconditions:**  
1) A pet with ID 124 does not exist in the system.  

**Steps:**  
1) Send a POST request to {{host}}//pet/124 with the following parameters:  
   name = "Updated name"  

**Expected Result:**  
1) Status code of the response: 404 Not Found.  
2) The response body contains a message text:  
   `"Pet not found."`  

---

### Test Case № 7:
**Title:** Check that the "name" field accepts special characters  


**Description:** Verify that the server correctly handles strings containing quotes and escapes special characters.  

**Preconditions:**  
1) The pet's initial data in the database is as follows  
   id = 123,  
   name = "Mur",  
   status = "available"  

**Steps:**  
1) Send a POST request to {{host}}//pet/123 with the following parameters:  
   name = "L'enomancer"  

**Expected Result:**  
1) Status code of the response: 200 OK.  
2) The name field of the pet with ID 123 is updated in the database to "L'enomancer".  

**Comment:** The requirements for acceptable special characters are unclear. This test assumes that quotes (`'`) and similar symbols are allowed.  

---

### Test Case № 8:
**Title:** Check the name field for UTF-8 encoding  

**Description:** Verify that the name field supports UTF-8 characters, including symbols from different languages (e.g., Chinese, Arabic, Japanese).  

**Preconditions:**  
1) The pet's initial data in the database is as follows  
   id = 123,  
   name = "Mur",  
   status = "available"  

**Steps:**  
1) Send a POST request to {{host}}//pet/123 with the following parameters:  
   name = "张伟اختبارテスト"  

**Expected Result:**  
1) Status code of the response: 200 OK.  
2) The name field of the pet with ID 123 is updated in the database to `"张伟اختبارテスト"`.  

**Comment:** Requirements for encoding support need clarification. This test assumes UTF-8 encoding is required.  
