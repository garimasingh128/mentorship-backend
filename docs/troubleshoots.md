# Troubleshoots

## Setting up Gmail to be used as default mail server in .env

Gmail required applications that will use their service to be authorized first beforehand. Failure in doing this will cause SMTP sending mail process fail with the response **"534-5.7.9 Application-specific password required..."**.

To solve this issue, you need to give this application an App password that is generated from Gmail account.

Here are the steps:

1. Go to https://myaccount.google.com/intro and login to your Gmail account. Then click on **Security** tab from the top navbar.
![security_tab_option](https://user-images.githubusercontent.com/29667122/80849819-46260c80-8c5c-11ea-977e-5a0f873437ac.png)
You will see this section:
![signing_in_settings_gmail_original](https://user-images.githubusercontent.com/29667122/80807468-a1c2ac80-8c00-11ea-9053-7e6759f4c7e6.png)

2. In the section *Signing in to Google* select **2-step verification** and follow the prompts to turn it ON.
3. Once step 2 completed, go back to Security page and from the same section (*Signing in to Google*) select **App password**.
![signing_in_settings_gmail_2steps_on](https://user-images.githubusercontent.com/29667122/80807613-07af3400-8c01-11ea-881c-fb2944e080d4.png)

4. Under *Select the app and device you want to generate the app password for.*:
- for *Select app* choose **Mail**
- for *Select device* choose **Other (Custom name)** then type **MentorshipSystem** (or choose any name you like)
![setting_gmail_app_passwords](https://user-images.githubusercontent.com/29667122/80807751-53fa7400-8c01-11ea-9f66-7be59af6c8fb.png)

5. Once you completed step 3 above, a window will open and show the autogenerated password that you can use for the application. Copy paste this code to your .env as the value for **APP_MAIL_PASSWORD**. Click done on the open window (back to Gmail account window), then you will see it on the **App passwords** list.
![gmail_new_app_password_in_list](https://user-images.githubusercontent.com/29667122/80807814-78eee700-8c01-11ea-8120-6c0e6f0997ba.png)

6. Make sure you have your **MAIL_SERVER** config in the `.env` set to **smtp.gmail.com** and both **MAIL_DEFAULT_SENDER** and  **APP_MAIL_USERNAME** set to the Gmail account you just authorized the app with.

7. Save and run the python script again from the command line: `python run.py`. Then try to register a new user on the Swagger UI. This should give HTTP response 200 (successful).
