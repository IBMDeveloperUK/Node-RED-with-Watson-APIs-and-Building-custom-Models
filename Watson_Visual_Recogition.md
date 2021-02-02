## Step 1 (Optional)

A Node-RED Flow editor opens with an empty panel named Flow 1. 

Rename your Flow via the menu to IBM Node-RED Lab. Click Done. 

![](Images/Rename.png)

 ## Step 2 
 
In the left navigation pane of the Editor you will see a lot of standard Node-RED nodes. At the end of the list there are certain categories already customized by IBM, such as `IBM_Watson`. 

As a first step, 
From the input category of nodes drag the ![](Images/http_image.png) node and drop it on the editor pane. 

When you click on each node to highlight it,the 'Info' tab on the right navigation pane will give you some information about the selected node. 
 
 ![](Images/HTTP.png)
 
 ## Step 3 
 
 Double click the http input node and specify the Method as a http GET request .Specify a name for your url which in this case is /reco
 You will be able to access the endpoint by removing everything after appdomain.cloud/ in your URL, and replacing it with /reco
 
 Click Done once completed. 

![](Images/Reco.png) 

 ## Step 4
 
 As you might have noticed, all the nodes are classified into different categories on the left pane. 
 From the 'function' nodes drag a ![](Images/Switch_Image.png) node and drop it on the editor pane. 
 
 Select the output of the /reco node and drop it on the input of the switch node.  
 
 ![](Images/Switch.png) 
 
 ## Step 5 
 
 Double click the switch node and enter the info shown on the following image and click Done.
 
 ![](Images/Swtich_Details.png) 
 
 ## Step 6 
 
From the function section of nodes drag a 'template' ![](Images/Template.png)  node and drop it on the editor pane and connect the “is null” output of the switch to the input of the template.



Double click the template and specify the following information: 

 1.	Name: Get Image URL
 2. Leave property as msg.payload
 3. Syntax Highlight: HTML 
 4. Format: Moustache template Template: 
 5. Paste the following code in the Template field

```

    <style>
input[type=submit]{
    background-color: rgb(85,150,230);
    border: none;
    color: white;
    padding: 16px 32px;
    text-decoration: none;
    margin: 4px 2px;
    cursor: pointer;
    font-size: 15px;
    border-radius: 10px;
)
input[type=text] {
    width: 50em;  height: 3em;
}
</style>
<script type="text/javascript">
function clicked(address) {
 var form = document.getElementById("imageform");
 document.getElementById('imageurl').value = address.src;
 form.submit();
}
</script>
<h1>Watson Visual Recognition on Node-RED</h1>
 <h2>Click an Image </h2>
 <form  action="{{req._parsedUrl.pathname}}" id="imageform">
 <img src="https://images.unsplash.com/photo-1570171278960-d6c2b316f3b1?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=800&q=60" height='100'
onclick="clicked(this)"/>
 <img src="https://images.unsplash.com/photo-1568198473832-b6b0f46328c1?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1592&q=80" height='100'
onclick="clicked(this)"/>
 <img src="https://images.unsplash.com/photo-1551717743-49959800b1f6?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1647&q=80" height='100'
onclick="clicked(this)"/>
 <img
src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/50/Queen_Elizabeth_II_March_2015.jpg/4
55px-Queen_Elizabeth_II_March_2015.jpg" height='100' onclick="clicked(this)"/>
 <h2>or paste an URL from the internet</h2>
        <input type="text" name="imageurl" id="imageurl"/><br>
        <input type="submit" value="Analyze"/>
</form> 

```

Click Done once completed

![](Images/Get_Image_URL.png) 


## Step 7

Add a 'Function' node (named Extract img URL) to convert the imageurl JSON object to a string and assign it to the payload to be provided as input to the Visual Recognition node. 

Changes should look as follows


![](Images/Extract_URL.png) 

![](Images/Extract_URL_Nodes.png) 



## Step 8

From the IBM_Watson category select the ![](Images/Visual_Recognition_Image.png) node and drop it behind the change node (Extract Image URL) from the previous step. Double click the Visual Recognition node and enter your API key you have created for the Visual Recognition service and change the Service Endpoint as shown below. Click Done

![](Images/Visual_Rec_Enpoint.png) 

![](Images/Visual_Rec_Image.png)

## Step 9 

Add another ![](Images/Template.png) Node behind the Visual Recognition node. Double Click the Template Node to Edit with fields mentioned below

1)  Name: Report 
2)  property: message.payload 
3)  Syntax Highlight: mustache 
4)  Format: Mustache template 

5) Template (paste the following code in the template field)

```
<div align="center">
    <form  action="{{req._parsedUrl.pathname}}">
        <input type="submit" value="Try again"/>
    </form>
<h1>Node-RED Watson Visual Recognition output</h1> <p>Analyzed image: {{req.query.imageurl}}<br/><img src="{{req.query.imageurl}}" height='200'/></p> <p><b>Here are my results:</b></p> {{#result.images}} 
        {{#classifiers}}
            <table border="0">
            <tr><td class=classifier colspan="2">{{classifier_id}}</td></tr>
                <tr><td class="title">Class</td><td class="title">Score</td></tr>
                {{#classes}}
                <tr><td><b>{{class}}</b></td><td><i>{{score}}</i></td></tr>
                {{/classes}}
            </table>
        {{/classifiers}}
    {{/result.images}}
</div>

```
Click Done. 

### Optional Styling to add at the top of the template field (before the code pasted in the previous step) 

``` 
<style> 

h4 { 
    text-align: center;
    margin: 10px;
}
table {
    width: 480px;
    margin-top: 10px;
}
th, td {
    padding: 8px;
    text-align: left;
    border-bottom: 1px solid #ddd;
    background-color: #FFFFFF;
    width: 50%;
}
.classifier {
    background-color: rgb(85,150,230);
    text-align: center;
}
.title {
    background-color:LightGrey;
}
input[type=submit]{
    background-color: rgb(85,150,230);
    border: none;
    color: white;
    padding: 16px 32px;
    text-decoration: none;
    margin: 4px 2px;
    cursor: pointer;
    font-size: 15px;
    border-radius: 10px;
) 

</style>

``` 

## Step 10

As the final node add a ![](Images/http_respone.png)  name it HTTP Response, and connect it as shown in the following picture. 

Add Optional Debug nodes as required which display the output of the node in the right side bar on the debug tab. 

![](Images/Final_nodes.png)


## Step 11 
Click the ![](Images/Deploy.png) button at the top of the Node-RED application to deploy the flow in your environment. 


## Step 12 

### Test the flow by calling the url http://'yourNode-REDHost'.cloud/reco 
 
 
Click on one of the images or Copy and Paste any image URL from the internet and click Analyse for your Visual Recognition Output

