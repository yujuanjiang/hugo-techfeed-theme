---
title: "How to Create Hugo Contact Form with Google Forms (FREE!)"
date: 2022-05-23T13:07:12-04:00
draft: false
---

<h5> Pre-requisite: </h5>
<ul>
<li>A google account </li>
<li>A website created off Hugo template </li>
</ul>
<br>

First, create a contact form with <a href="https://docs.google.com/forms">Google form</a>, and get the field name for each required field of the form by inspecting webpage elements (usually they start with <em>"entry:"</em>).

  ![Google form example](/how_to_create_hugo_contact_form_with_google_forms/googleForm.png)

Get the google form id: <br><br>
Click the "Send" button on top right, and select  to get the Google form id from its pre-filled link (the 56 digit letter & number string between <em>"d/e/"</em> and <em>"/viewForm"</em>).

  ![Get google form id](/how_to_create_hugo_contact_form_with_google_forms/getlink.png)

N.B.: It's recommended to turn on email notification so Google can notify you once a new contact request is submitted. <br>
Also, it'd be better toggle off <em>"Collect email address"</em> (otherwise the field name is not populated - no idea why) and <em>"Limit to 1 response"</em> for the visitor's convenience.

  ![Turn on email notification](/how_to_create_hugo_contact_form_with_google_forms/emailnotif.png)

  ![Toggle off](/how_to_create_hugo_contact_form_with_google_forms/toggles.png)

Next, let's create a contact form on your Hugo website. <br><br>
This can be done however you like - it's simple html + css, but this form has to be consisted of the same fields as your google form! <br><br>

(You can even copy directly the google form source code, but it's preferably to keep the consistent style with the whole Hugo theme.) <br><br>
For example, if your google form contains 4 fields - name/email/subject/message, your Hugo contact form should have the same 4 fields.

A simple example would be like:

>>
    <form action="https://docs.google.com/forms/d/e/<YOUR FORM ID>/formResponse" method="post" target="hidden_iframe" onsubmit="submitted=true">
    <label>Name</label><input type="text" placeholder="Name*" class="form-input" name="<GOOGLE FORM FIELD ID1>" required>
    <label>Email*</label>
        <input type="email" placeholder="Email address*" class="form-input" name="<GOOGLE FORM FIELD ID2>" required>
    <label>Subject*</label>
        <input type="text" placeholder="Subject*" class="form-input" name="<GOOGLE FORM FIELD ID3>" required>
    <label>Type your message here...</label>
        <textarea rows="5" placeholder="Message" class="form-input" name="<GOOGLE FORM FIELD ID4>" ></textarea>
    <button type="submit">Send</button>
    </form>

<br>
Now let's apply google form field ids to your Hugo contact form! <br><br>
You can assign the ids into form html code directly, or create corresponding parameters in file <em>""/config/_default/params.toml"</em> and refer to them in your html code. <br>

  ![Assign google form ids to your Hugo contact form](/how_to_create_hugo_contact_form_with_google_forms/idMapping.png)

Then we can submit the form to Google by changing its form "action" to Google form. <br>

This way, Google will assume the post request came from the google form your created earlier and will handle the response for us (free work lol).

>>
    <form action="https://docs.google.com/forms/d/e/<YOUR GOOGLE FORM ID>/formResponse" method="post" target="hidden_iframe" onsubmit="submitted=true;">

<br>

It's pretty much finished now, but in order to have a better user experience it's recommended to create a "Thank you" page inside your Hugo website. <br>
Otherwise after your visitor submitted the form she/he will be redirected to Google's defautl "Thank you" page. <br>

Simple createa page using command "Hugo new thankyou.md". <br>
Inside the thankyou.md file put however you want to greet to your visitors like <em>"Thank you! I will get back to you asap.". </em> <br><br>
You simply need to add below code right before your form tag:

>>
    <iframe name="hidden_iframe" id="hidden_iframe" style="display:none;" onload="if(submitted) {window.location='/thankyou';}"></iframe>

<br><br>
... and update "form target" to this "hidden_iframe":

>>
    <form action="https://docs.google.com/forms/d/e/<YOUR GOOGLE FORM ID>/formResponse" method="post" target="hidden_iframe" onsubmit="submitted=true;">

<br><br>
VOILA! Once the visitor submit a contact form she/he will see below page:

  ![Thank you page](/how_to_create_hugo_contact_form_with_google_forms/thankyou.png)

N.B.: this static form does *NOT* validate the data. <br>
So if the email format is not correct ("\*\*\*@\*\*\*.\*\*") the contact page will still return "Thank you!" but Google will ***NOT*** be able to capture this response. <br>
You can add some extra validation logic with JavaScript to prevent such issue. <br>

<br>

OK. <br><br>
Now if someone wants to contact you and input all the required information, you will receive an email notification from Google. Also, you can check all responses received on Google form "Response" tab:

  ![Google response tab](/how_to_create_hugo_contact_form_with_google_forms/responsetab.png)

<br><br>
Enjoy blogging! :)
