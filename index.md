  <html xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
    <head>
      <title>Test Messaging | Salesforce</title>
      <apex:slds />
      <style type="text/css">
            @font-face {
                font-family: ITC Avant Garde;
                src: url(https://a.sfdcstatic.com/shared/fonts/avant-garde/4c0a2f1e-8b66-47d8-8e7c-9b259c4d363f.woff2) format("woff2"),url(https://a.sfdcstatic.com/shared/fonts/avant-garde/f8c88707-ed03-43dd-aec9-29571c329bcc.woff) format("woff");
                font-weight: 400
            }
            
            body {
                background: #EAF5FE;
                font-family: system-ui;
            }
            
            #bgImage {
                min-height: 100%;
                min-width: 1024px;
                width: 100%;
                height: auto;
                position: fixed;
                top: 350px;
                left: -64px;
                background-image: url(/projRes/ui-admin-success-components/img/easy-onboarding-bg.jpg);
                background-repeat: no-repeat;
                background-size: cover;
                z-index: -99999;
            }
            #mainContainer {
                margin-top: 34px;
                margin-left: 34px;
            }
            
            #bodyContainer {
                margin-left: 30px;
            }
            
            #bodyContainer h1 {
                font-family: ITC Avant Garde;
                font-weight: 600;
                font-size: 48px;            
                color: #032D60;
            }
            
            #bodyContainer ol {
                list-style: decimal;
            }
            
            #bodyContainer ol li {
                margin-left: 0px;
                margin-bottom: 16px;
                font-weight: 500;
                font-size: 16px;
                line-height: 24px;
                color: #001639;
            }

            #accordion {
                background-color: #eee;
                width: 75%;
                cursor: pointer;
                padding: 15px;
                margin-top: 10px;
                border: none;
                border-radius: 10px;
                text-align: left;
                outline: none;
                transition: 0.4s;
            }

            #accordion img {
                display: inline;
                width: 16px;
                margin-right: 10px;
            }

            .active, #accordion:hover {
                background-color: #ccc; 
            }

            #accordion .chevrondown {
                display: none;
            }

            #accordion.active .chevronright {
                display: none;
            }

            #accordion.active .chevrondown {
                display: inline;
            }

            #videoDemoContainer {
                margin: 20px 0px;
                width: 330px;
                height: 452px;
                display: none;
            }
        </style>

        <script type="text/javascript" async="true" src="https://play.vidyard.com/embed/v4.js"></script>
    </head>
    <body>
      <div id="bgImage"></div>
      <div id="mainContainer">
          <div id="logoContainer">
              <img id="logo" src="https://c1.sfdcstatic.com/content/dam/sfdc-docs/www/logos/logo-salesforce.svg" width="65px" alt="Salesforce logo" />
          </div>
          <div id="bodyContainer">
              <h1>Test Your Messaging Deployment</h1>
              <ol>
                  <li>In the previous browser tab where you’re signed into Salesforce, open the agent console.</li>
                  <li>In the Omni-Channel utility or sidebar, make yourself available to accept incoming messaging sessions.<br />
                     <button id="accordion">
                        <img class="chevronright" src="/apexpages/slds/latest/assets/icons/utility/chevronright_60.png"/>
                        <img class="chevrondown" src="/apexpages/slds/latest/assets/icons/utility/chevrondown_60.png"/>
                        Show Me Where
                     </button>
                     <div id="videoDemoContainer">
                        <img
                            style="display: block; max-width: 330px; max-height: 452px;"
                            class="vidyard-player-embed"
                            src="https://play.vidyard.com/6udN7LzkmqU8RgRvyoKDrS.jpg"
                            data-uuid="6udN7LzkmqU8RgRvyoKDrS"
                            data-v="4"
                            data-type="inline"
                            data-width="330"
                            data-height="452"
                        />
                     </div></li>
                  <li>In this tab, open the Messaging conversation window and send a message as a customer.</li>
                  <li>In Salesforce, accept the messaging session and send a response.</li>
                  <li>Chat back and forth, and then end the conversation.</li>
              </ol>
          </div>
          <div>
            <input placeholder="Category ID" id="categoryId"></input>
            <input placeholder="Product AI Question" id="prodAI"></input>
            <input placeholder="RCID" id="rcid"></input>
            <select id="origin">
                <option value="sales">Sales</option>
                <option value="commercial-sales">Commercial Sales</option>
                <option value="outlet">Outlet</option>
                <option value="premier">Premier Phase 1</option>
            </select>
          </div>
          <div style="margin: 10px 0px;">
                <label for="hot-customer">
                    <input type="checkbox" tabindex="0" id="hot-customer"></input>
                    <span>Hot Customer</span>
                </label>
                <label for="network-error">
                    <input type="checkbox" tabindex="0" id="network-error"></input>
                    <span>Network Error</span>
                </label>
          </div>
          <div>
            <button onclick="loadResources()">Load chat</button>
            <button onclick="loadChat()">Inititate chat</button>
          </div>
      </div>
      <script>
            var videoAccordion = document.getElementById("accordion");
            videoAccordion.addEventListener("click", function() {
            this.classList.toggle("active");

            var videoContainer = this.nextElementSibling;
            if (videoContainer.style.display === "block") {
                videoContainer.style.display = "none";
            } else {
                videoContainer.style.display = "block";
            }
        });
        </script>
    
      <script type='text/javascript'>
        var snapInObject = {
            name: "",
            emailAddress: "",
            languageCode: 'en',
            countryCode: 'us',
            sourceSite: window.location.href,
            categoryId: "",
            productAILastQuestion : ""
        };

        var origin = 'Sales';
        let hotCustomerCheckbox = false;
        let networkErrorCheckbox = false;
        let cobrowseCheckbox = false;
        async function loadChat () {
            var selectedEnv = 'miawpoc1';
            let selectedOrigin = document.getElementById('origin').value;

            let selectedLanguageDropdown = 'en';
            let selectedCountryDropdown = 'us';
            snapInObject.countryCode = selectedCountryDropdown;
            snapInObject.languageCode = selectedLanguageDropdown;
            // snapInObject.categoryId = '';
            // snapInObject.productAILastQuestion  = '';
            // let prechatStaticResource = '../../pages/ursa/js/DCSFPrechatCustomResource.js';

            let isHotCustomer = document.getElementById('hot-customer').checked;
            let isCoBrowseEnabled = false;
            if(isHotCustomer){
                snapInObject.name = 'Prechat Customer';
                snapInObject.emailAddress = 'prechat_customer@test.com';
            }

            snapInObject.isCoBrowseEnabled = isCoBrowseEnabled;
            if (selectedOrigin === 'sales') {
                let prechatStaticResource = `https://dcsf--miawpoc1.sandbox.my.salesforce-sites.com/liveAgentSetupFlow/resource/DellMIAWPrechatsvc/DellMIAWPrechatsvc/DellMIAWPrechatsvc.js`;
                await loadPrechatResource(prechatStaticResource);
                if (!localStorage.getItem("isChatActive")){

                    console.log("Loading Prechat",snapInObject);
                    console.log("dcsfPrechatResourceLoaded", sessionStorage.getItem("dcsfPrechatResourceLoaded"))
                    triggerPrechatResource(snapInObject);
                }
                else{
                    console.log("Chat pertsisted or prechat resource not loaded")
                }
            }
            else if (selectedOrigin === 'commercial-sales') {
                let prechatStaticResource = `https://dcsf--miawpoc1.sandbox.my.salesforce-sites.com/liveAgentSetupFlow/resource/DellMIAWCommSalesEmbeddedsvc/DellMIAWCommSalesEmbeddedsvc/DellMIAWCommSalesEmbeddedsvc.js`;
                await loadChatResource(prechatStaticResource);
                if (!localStorage.getItem("isChatActive")){

                    console.log("Loading comm sales file",snapInObject);
                    console.log("dcsfPrechatResourceLoaded", sessionStorage.getItem("dcsfPrechatResourceLoaded"))
                    triggerSnapin(snapInObject);
                }
                else{
                    console.log("Chat pertsisted or prechat resource not loaded")
                }
            }
            else if (selectedOrigin === 'outlet') {
                let prechatStaticResource = `https://dcsf--miawpoc1.sandbox.my.salesforce-sites.com/liveAgentSetupFlow/resource/DellMIAWOutletEmbeddedsvc/DellMIAWOutletEmbeddedsvc/DellMIAWOutletEmbeddedsvc.js`;
                await loadChatResource(prechatStaticResource);
                if (!localStorage.getItem("isChatActive")){

                    console.log("Loading outlet file",snapInObject);
                    console.log("dcsfPrechatResourceLoaded", sessionStorage.getItem("dcsfPrechatResourceLoaded"))
                    triggerSnapin(snapInObject);
                }
                else{
                    console.log("Chat pertsisted or prechat resource not loaded")
                }
            }
            else if (selectedOrigin === 'premier') {
                let rcid = document.getElementById('rcid').value;
                let prechatStaticResource = `https://dcsf--miawpoc1.sandbox.my.salesforce-sites.com/liveAgentSetupFlow/resource/DellMIAWPremierEmbeddedsvc/DellMIAWPremierEmbeddedsvc/DellMIAWPremierEmbeddedsvc.js`;
                await loadChatResource(prechatStaticResource);
                if (!localStorage.getItem("isChatActive")){
                    snapInObject.rcid = rcid;
                    console.log("Loading premier file",snapInObject);
                    console.log("dcsfPrechatResourceLoaded", sessionStorage.getItem("dcsfPrechatResourceLoaded"))
                    triggerSnapin(snapInObject);
                }
                else{
                    console.log("Chat pertsisted or prechat resource not loaded")
                }
            }
            // snapInObject.categoryId = snapInObject.languageCode === 'en' && (snapInObject.countryCode === 'us' || snapInObject.countryCode === 'ca') ? 'access-platforms' : '';
            
            //Chat Persistence check
            // if (!localStorage.getItem("isChatActive") && (sessionStorage.getItem("dcsfPrechatResourceLoaded")==1)){
        }
        function loadChatResource(src) {
            return new Promise((resolve, reject) => {
                let resource = document.createElement("script")
                if (!sessionStorage.getItem("dcsfChatResourceLoaded")) { sessionStorage.setItem("dcsfChatResourceLoaded", 0) }
                // let count = (Number(sessionStorage.getItem("dcsfResourceLoaded")) + 1)
                resource.type = "text/javascript"
                resource.src = src + "?v=" + Date.now()

                resource.onload = function () {
                    console.log("Chat file loaded", src),
                        sessionStorage.setItem("dcsfChatResourceLoaded", 1),
                        resolve();
                }
                resource.onerror = function () {
                    console.log('chat resource not loading');
                    reject
                }
                document.getElementsByTagName("body")[0].appendChild(resource);
            })
        }
        function loadPrechatResource(src) {
            return new Promise((resolve, reject) => {
                let resource = document.createElement("script")
                
                resource.type = "text/javascript"
                resource.src = src + "?v=" + Date.now()

                resource.onload = function () {
                    console.log("Prechat file loaded", src),
                        // sessionStorage.setItem("dcsfPrechatResourceLoaded", 1),
                        resolve();
                }
                resource.onerror = function () {
                    console.log('Prechat resource not loading');
                    reject
                }
                document.getElementsByTagName("body")[0].appendChild(resource);
            })
        }
        async function loadResources () {

            // let chatStaticResource = "../../pages/ursa/js/DellEmbeddedsvcZHCN.js";
                let selectedEnv = 'miawpoc1';
                let selectedOrigin = document.getElementById('origin').value;


                if (selectedOrigin === 'sales') {
                    let isNetworkError = document.getElementById('network-error').checked;
                    let isCoBrowseEnabled = false;
                    // let isHotCustomer = document.querySelector("#hot-customer-checkbox > label > input").checked;
                    // if(isHotCustomer){
                    //     snapInObject.name = '';
                    //     snapInObject.emailAddress = '';
                    // }

                    let selectedLanguageDropdown = 'en';
                    let selectedCountryDropdown = 'us';
                    var category = document.getElementById('categoryId').value || '';
                    var productAI = document.getElementById('prodAI').value || '';
                    console.log(category, 'category value');
                    console.log(productAI, 'productAI value');
                    let chatStaticResource = `https://dcsf--miawpoc1.sandbox.my.salesforce-sites.com/liveAgentSetupFlow/resource/DellMIAWEmbeddedsvc/DellMIAWEmbeddedsvc/DellMIAWEmbeddedsvc.js`;

                    snapInObject.countryCode = selectedCountryDropdown;
                    snapInObject.languageCode = selectedLanguageDropdown;
                    snapInObject.categoryId = category;
                    snapInObject.isCoBrowseEnabled = isCoBrowseEnabled;
                    snapInObject.productAILastQuestion  = productAI;

                    // snapInObject.categoryId = snapInObject.languageCode === 'en' && (snapInObject.countryCode === 'us' || snapInObject.countryCode === 'ca') ? 'access-platforms' : '';
                    console.log("Selected",selectedCountryDropdown," ",selectedLanguageDropdown," ",origin);

                    if (!isNetworkError) {
                        await loadChatResource(chatStaticResource);
                        triggerSnapin(snapInObject);
                    }
                }


            } 
            window.addEventListener('onChatRequestSuccess', function (e) { console.log("onChatRequestSuccess and SessionKey", e.detail.sessionKey); localStorage.setItem("isChatActive", true);});
            window.addEventListener('afterDestroy', function (e) { console.log("addEventListener", e); localStorage.removeItem("isChatActive"); });
            window.addEventListener('onChatEndedByChasitor', function (e) { console.log("addEventListener", e); localStorage.removeItem("isChatActive"); });
            window.addEventListener('onChatEndedByAgent', function (e) { console.log("addEventListener", e); localStorage.removeItem("isChatActive"); });
            window.addEventListener('afterMaximize', function (e) { console.log("addEventListener", e)});
            window.addEventListener('afterMinimize', function (e) { console.log("addEventListener", e) });
            window.addEventListener('onChatTransferSuccessful', function (e) { console.log("addEventListener", e) });
            window.addEventListener('onAgentMessage', function (e) { console.log("addEventListener", e) });
            window.addEventListener('onChatReconnectSuccessful', function (e) { console.log("addEventListener", e) });
            window.addEventListener('onConnectionError', function (e) { console.log("addEventListener", e) });
            window.addEventListener('onChatEstablished', function (e) { console.log("addEventListener", e) });
            window.addEventListener('onChatEndedByChatbot', function (e) { console.log("addEventListener", e); localStorage.removeItem("isChatActive");  });
        </script>

    </body>
  </html>
