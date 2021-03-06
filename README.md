# angular-inquiry-form-with-recaptcha

日本語の解説は[AngularとBootstrapで問い合わせフォーム](https://nanbu.marune205.net/2022/05/angular-bootstrap-inquiry-form-recaptcha.html?m=1)にあります

Angular project of inquiry form.  optional reCAPTCHAv3.

![app sample image](https://github.com/sugakenn/angular-inquiry-form-with-recaptcha/blob/main/docs/2022y05m27d_161841484.jpg)

## Quick Start
### 1.[copy folder from dist/inquiry-form/en-US(or ja) to htdocs(if you use apache server)](dist/inquiry-form)
### 2.[copy receive-message.php from src/backend/ to same dir](src/backend/)
### 3.When someone accesses /en-US(or ja)/index.html and sends a message, the message is stored in htdocs/(locale)/message dir.

## Angular Project
### These codes are Angular project.

#### compile option
 - en-US,ja build
   
   ng build --configuration="production" --localize --base-href=../
 - ja build
 
   ng build --configuration="ja" --localize --base-href=../
 - normal build is en-US build
 
## Back end
Use PHP for the backend.Basically, the behavior of this code is just to save the POSTed JSON data as it is.

Because php_mbstring.dll is set in the development environment, <strong>Please set php_mbstring.dll when using. </strong>

There are some validations for security reasons.

- Remote Address Check
  - If you create a dir named "access" with htdocs, the number of transmissions will be checked for each IP address.
 You can set the number and interval in the PHP file. And You also can change dir name.
  - Invalid List Check
    - If you create an invalid.v4 file and include the IP address in the list, the host will not be able to send messages.

      The Format is 000-000-000-000 separated by \n
      
      Example 10.8.100.1 :point_right: 010-008-100-001
      
    - invalid.v6 is IPv6 version file. In this file, compare network address. This Format is 0000-0000-0000-0000 separated by \n

      Example 2001 : : 1 : a : b : c : d :point_right: 20001-0000-0000-0001 (cut the : a : b : c : d)
    
    - Comment out is not judged, but lines that do not follow the format are ignored as a result of collation
      
  - XSRF Check
  
     Angular's HttpClient has XSRF validation.So, the implementation is written in PHP.
  - reCAPTCHA 
   

## reCAPTCHA

You can use [Google's reCAPTCHA v3](https://www.google.com/recaptcha/about/) by using [ng-recaptcha](https://github.com/DethAriel/ng-recaptcha) 

You can use it by getting two passwords from Google and adding them to your code.

The settings are commented out, so please describe them as necessary.
- app.module.ts line(7,18,21)
- app.component.ts line(5,18,79-132)
- receive-message.php line(27-30)
