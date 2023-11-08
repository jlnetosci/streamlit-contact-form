# Streamlit Contact Form Template

![contact-form](/img/screenshot.png)
[Live Demo](https://contact-form-template.streamlit.app/contact-form)

## About
This repository contains `pages/contact-form.py`, a contact form template for Streamlit apps. While there are alternatives using external tools, this project exclusively utilizes python libraries and Streamlit elements, making it integrate with your app seamlessly.

The template contains e-mail validation using [email-validator](https://pypi.org/project/email-validator/) and customizable CAPTCHA generation through python's [captcha](https://pypi.org/project/captcha/) library. Messages are processed using the [smtplib](https://docs.python.org/3/library/smtplib.html) SMTP protocol client.

Messages will be directed to an email address of your choice, and you have the option to simultaneously send a confirmation to the messaging user's provided contact email.

For a smoother setup and configuration, I recommend having some familiarity with Streamlit [multipage apps](https://docs.streamlit.io/library/get-started/multipage-apps/create-a-multipage-app), and how Streamlit manages [secrets](https://docs.streamlit.io/streamlit-community-cloud/deploy-your-app/secrets-management) when deploying an app.

## Setup

To turn `pages/contact-form.py` into a fully functioning contact form, uncomment the lines relative to "Email configuration" (v0.2.0, lines 91-129): 

``` python                   
#smtp_server = server
#smtp_port = port
#smtp_username = u
#smtp_password = secret
#recipient_email = recipient

## Create an SMTP connection
#server = smtplib.SMTP(smtp_server, smtp_port)
#server.starttls()
#server.login(smtp_username, smtp_password)

## Compose the email message
#subject = "Contact Form Submission" # subject of the email you will receive upon contact.
#body = f"Email: {email}\nMessage: {message}"
#msg = MIMEMultipart()
#msg['From'] = smtp_username
#msg['To'] = recipient_email
#msg['Subject'] = subject
#msg.attach(MIMEText(body, 'plain'))

## Send the email
#server.sendmail(smtp_username, recipient_email, msg.as_string())

## Send the confirmation email to the message sender # If you do not want to send a confirmation email leave this section commented
#current_datetime = datetime.datetime.now()
#formatted_datetime = current_datetime.strftime("%Y-%m-%d %H:%M:%S")
#confirmation_subject = f"Confirmation of Contact Form Submission ({formatted_datetime})"
#confirmation_body = f"Thank you for contacting us! Your message has been received.\n\nYour message: {message}"
#confirmation_msg = MIMEMultipart()
#confirmation_msg['From'] = smtp_username
#confirmation_msg['To'] = email  # Use the sender's email address here
#confirmation_msg['Subject'] = confirmation_subject
#confirmation_msg.attach(MIMEText(confirmation_body, 'plain'))
#server.sendmail(smtp_username, email, confirmation_msg.as_string())

## Close the SMTP server connection
#server.quit()

#st.success("Sent successfully!") # Success message to the user.
```

and comment or delete the mock-up information (v0.2.0, lines 132-133):

``` python
st.info("""This would have been a message sent successfully!  
For more information on activating the contact form, please check the [documentation](https://github.com/jlnetosci/streamlit-contact-form).""") # Please delete this info box if you have the contact form setup correctly.
```

## Configuration

To successfully process messages, you will need to set up an SMTP server. You can do it using something as user-friendly as [Gmail](https://support.google.com/a/answer/176600?hl=en). I would recommend using a dedicated email address specifically for forwarding contact form messages.

When deploying your app [configure these variables](https://docs.streamlit.io/streamlit-community-cloud/deploy-your-app/secrets-management):

    OPTIONS: A string of characters that can be included in the CAPTCHA.
    SERVER: Your SMTP server address
    PORT: The port for your SMTP server.
    U: Your SMTP username.
    SECRET: Your SMTP password.
    RECIPIENT: The recipient email address where messages will be sent. 

For example: 

    OPTIONS = "ACDEFGHIJKLMNOQPRSTUVWXYZ123456789"
    SERVER = "smtp.gmail.com""
    PORT = 587
    U = "email-address-that-will-SEND-the-message@gmail.com"
    SECRET = "password-provided-by-gmail-for-use-in-apps"
    RECIPIENT = "your-email-address-that-will-RECEIVE-the-message@gmail.com"

## Customization

The form is highly customizable regarding appearance and text content. Feel free to make it your own if you use it in any capacity.

## Interact with the contact form

You can interact with this quasi-functional version (it will not actually send a contact message but will, in every other way, behave like the functional contact form) at https://contact-form-template.streamlit.app/.