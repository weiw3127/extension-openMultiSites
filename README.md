# extension_open_MultiSites
This repository demonstrates the powerful combination of browser extension and iframe. I'll use Google as an example. With this extension, I can open multiple websites from the Google search results pages with just a click. So when I am looking for something, I do not have to open on one result after another, I can now check them at a glance.

![demo of the extension](demo.gif)


## How it works: 
1. Make sure we are now under the domain google.com 
2. Enter search terms in the extension popup window, and break each term with a new line.
3. Click the button and the Google search results will appear one by one at the bottom of the website.

## Customize: 
- Change the src of iframe to get your own targeted page.

  ```
  iframe.src = googleUrl;
  ```
 
 - Add customized function to interact with the iframe. <br />
   For instance, in the 'content.js' I added a sample function 'generate' that locate and extract the titles of each search result
   
   ```
   let generate = function(query){
      const xpath = "descendant::h3";
      const idForFrame = "#scrapeTarget" + query.replace(/\s+/g, "");
      let results = document.querySelector(idForFrame).contentWindow.document.evaluate(xpath, document.querySelector(idForFrame).contentWindow.document, null, XPathResult.ANY_TYPE, null);
      let urlBank = [];
      let num = 0;
      let res;
      while (res = results.iterateNext()) {
        urlBank.push(res.textContent);
        num+=1;
      }
      return {urlBank, num};
    }
    ```
    Build any function that fit your needs. And don't forget to add it into the main function for extension
 
 ## How to install unpacked extensions: 
 Go to the extension page (chrome://extensions/) > click the developer mode (top right) > click on load unapacked (top left) > upload the entire folder 


 ## To update the unpacked extensions: 
 Click on the extension's reload button. <br /><br />
  <img width="425" alt="update" src="https://user-images.githubusercontent.com/19240127/139778521-6e2ffddd-9d69-4de7-ad34-eace16e76633.png">
 
