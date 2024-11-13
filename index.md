<body>
<script type='text/javascript'>
	function initEmbeddedMessaging() {
		try {
			embeddedservice_bootstrap.settings.language = 'en_US'; // For example, enter 'en' or 'en-US'

			embeddedservice_bootstrap.init(
				'00D3K0000000oqM',
				'TEST_WEB_CHAT',
				'https://dcsf--miawpoc1.sandbox.my.site.com/ESWTESTWEBCHAT1731519949066',
				{
					scrt2URL: 'https://dcsf--miawpoc1.sandbox.my.salesforce-scrt.com'
				}
			);
		} catch (err) {
			console.error('Error loading Embedded Messaging: ', err);
		}
	};
</script>
<script type='text/javascript' src='https://dcsf--miawpoc1.sandbox.my.site.com/ESWTESTWEBCHAT1731519949066/assets/js/bootstrap.min.js' onload='initEmbeddedMessaging()'></script>
</body>
