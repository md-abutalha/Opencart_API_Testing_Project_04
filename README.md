
# Opencart API Testing Project

I locally set up OpenCart and conducted API testing on essential cart functions, including adding products, viewing cart content, editing quantities, and removing items. These tests validated the API's efficiency in handling cart operations, ensuring a reliable user experience. The results were documented and reported using a Newman HTML report.




## Features of Opencart API Testing 

- Create Session/Token
- Add Product to Cart
- Cart Content
- Edit Product Quantity in Cart
- Remove Product Quantity in cart



## Opencart Build Deployment/Installation Locally

1) Opencart download location: 
https://www.opencart.com/index.php?route=cms/download
Click on previous releases
Recommended version: opencart-3.0.3.8

2) XAMPP for Apache, mysql, and php installation. 
Download Link: https://www.apachefriends.org/download.html
Recommended version: 7.4.29/PHP 7.4.29





## Xampp

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/SetUp/Xamamp%20set%20up.png)

## Step by step OpenCart Installation

- Copy opencart folder(Step1) in to below location. C:\xampp\htdocs
-  After copying rename the folder “ opencart “
- Rename files 
    Go to C:\xampp\htdocs\opencart\upload 
    Rename file 'config-dist.php' to 'config.php' 

    Go to C:\xampp\htdocs\opencart\upload\admin 
    Rename file 'config-dist.php' to 'config.php
- Connect to the database and create DB. 
DB Access URL: http://localhost/phpmyadmin/

- Create new database 'openshop' (Refer the    screenshots below to create new Database in MySQL)

## Database SetUp

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/SetUp/create_database.png)

- Open the site http://localhost/opencart/ Click on upload

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/SetUp/open_site_localhost-3.png)

- Navigate to http://localhost/opencart/upload/install/index.php, Click on CONTINUE Button....

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/SetUp/Navigagte%20to%20continue-4.png)

- If you are getting above error GD is off in set up  then you have to do below steps.

    Open XAMPP Control panel, 
    click on config button for Apache then open PH (php.ini) file
    Add new entry in the php.ini file extension=gd
    Then stop and start Apache server.

- Click on continue
  Provide Database connection details

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/SetUp/set_up_configuration-5_db.png)

- Go to location C:\xampp\htdocs\opencart\upload 
    Delete install folder
- Go to Application URL
    Frontend application URL: http://localhost/     opencart/upload/

- Backend Application url: http://localhost/opencart/upload/admin/


## In The Collection Variable set

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/module_variable.png)

## Create Session/Token In Postman Request 

Create Session in Request (POST)

```bash
  url: {{baseUrl}}api/login
  key generate: 

  Script: 
  pm.test("Status code is 200", () => {
    pm.response.to.have.status(200);
});

//capturing response response
 var jsonData = pm.response.json();

//Validating JSON response 
pm.test("checking success msg in response", () => {
    pm.expect(jsonData.success).to.eql("Success: API session successfully started!");
   
});

//creating collection variable to store api_token
pm.collectionVariables.set("api_token_val",jsonData.api_token)

response: 

{
    "success": "Success: API session successfully started!",
    "api_token": "b5e77de14dd8c52fdfe94df1a6"
}
```

## Create Session Body

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/create_session-1/session_body.png)

## Test Script & Respone

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/create_session-1/session_script_generate_toeken-2.png)

## Add Product to cart In Postman Request 

Add Product to cart test script in Request (POST)

```bash
  Pre-Request: 

  pm.collectionVariables.set("product_id","40");
  pm.collectionVariables.set("quantity","2");

```
```bash
  Post-Request: 

    pm.test("Status code is 200", () => {
    pm.response.to.have.status(200);
    });


    //Validating JSON response 
    pm.test("checking success msg in response", () => {
    var jsonData = pm.response.json();
    pm.expect(jsonData.success).to.eql("Success: You    have modified your shopping cart!");
   
});

```
## Add to cart Param

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/add_product_to_cart-2/add_product_cart_param-1.png)

## Add to cart Authorization

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/add_product_to_cart-2/add_product_cart_param-1.png)


## Add to cart Body

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/add_product_to_cart-2/add_product_body-3.png)


## Add to cart Script

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/add_product_to_cart-2/add_product_test_script-4.png)



## Cart Content (Get Request)

 cart Content test script in Request (POST)

```bash
 Post-Script: 

 pm.test("Status code is 200", () => {
    pm.response.to.have.status(200);
});

var jsonData=JSON.parse(responseBody);
pm.environment.set("cart_id_key",jsonData.products[0].cart_id);

```

## Cart Content Body

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/cart_content-3/cart_content_body-1.png)


## Cart Content Test Script

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/cart_content-3/cart_content_test_script-2.png)

## Edit Product quantity in Cart

 Edit Product quantity in cart test script in Request (POST)

```bash
pm.test("Status code is 200", () => {
    pm.response.to.have.status(200);
});

//Validating JSON response 
pm.test("checking success msg in response", () => {
     var jsonData = pm.response.json();
    pm.expect(jsonData.success).to.eql("Success: You have modified your shopping cart!");
   
});

```
## Edit Product Quantity Body

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/edit_product_quantity-4/edit_product_quantity_body-1.png)

## Edit Product Quantity Test Script

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/edit_product_quantity-4/edit_product-quantity_test-2.png)


## Remove Product from cart

 Remove product test script in Request (POST)

```bash
pm.test("Status code is 200", () => {
    pm.response.to.have.status(200);
});

//Validating JSON response 
pm.test("checking success msg in response", () => {
     var jsonData = pm.response.json();
    pm.expect(jsonData.success).to.eql("Success: You have modified your shopping cart!");
   
});

//Un-set collection variables
pm.collectionVariables.unset("api_token_val")
pm.collectionVariables.unset("product_id")
pm.collectionVariables.unset("quantity")
pm.environment.unset("cart_id_key");


```

## Remove Cart Body

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/remove_product-from_cart-5/remove_cart_body-1.png)

## Remove Cart Test Script

![App Screenshot](https://raw.githubusercontent.com/md-abutalha/Opencart_API_Testing_Project_04/master/opencart_screenchots/remove_product-from_cart-5/remove_test_script-2.png)

## Newman HTML Report

[New Man HTML Report](newman-run-report-2024-08-28-04-37-34-456-0.html)

## Postman API Documentation

[Postman API Testing Documentation](https://documenter.getpostman.com/view/37041522/2sAXjJ5YNf)

## Authors

- [@abutalha](https://github.com/md-abutalha)


## 🔗 Links
[![portfolio](https://img.shields.io/badge/my_portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://github.com/md-abutalha)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/abu-talha1/)
[![twitter](https://img.shields.io/badge/twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://x.com/abu_talha0x)



