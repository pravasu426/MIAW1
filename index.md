<!DOCTYPE html>

<HTML>
	<head>
    <meta charset="UTF-8">
    
    <!-- Content Security Policy in a meta tag -->
    <meta http-equiv="Content-Security-Policy" content="frame-ancestors 'self' https://dcsf--miawpoc1--c.sandbox.vf.force.com ;">
    
    
</head>
<body>
	

<script type='text/javascript'>
	function initEmbeddedMessaging() {
		try {
			embeddedservice_bootstrap.settings.language = 'en_US'; // For example, enter 'en' or 'en-US'

			embeddedservice_bootstrap.init(
				'00D3K0000000oqM',
				'DELL_CONNECT_MIAW_VF',
				'https://dcsf--miawpoc1.sandbox.my.site.com/ESWDELLCONNECTMIAWVF1730786036962',
				{
					scrt2URL: 'https://dcsf--miawpoc1.sandbox.my.salesforce-scrt.com'
				}
			);
		} catch (err) {
			console.error('Error loading Embedded Messaging: ', err);
		}
	};
</script>
<script type='text/javascript' src='https://dcsf--miawpoc1.sandbox.my.site.com/ESWDELLCONNECTMIAWVF1730786036962/assets/js/bootstrap.min.js' onload='initEmbeddedMessaging()'></script>

</body>
</HTML>
