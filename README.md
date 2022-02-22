Starting with v2.0, submissions need to be made using [Submission UI](http://submissions-ui.mlcommons.org/index)
Usage

1. Before the submission process begins you will receive an email containing an ID (Submitter ID). You will need this in order to upload your results. (This information will be sent to the email you provided in the registration survey). A link to access the web UI will also be provided.
[Image](assets/images/index.png)
2. Using this interface, enter the ID that was provided to you, select the appropriate benchmark, and upload from your computer an encrypted tarball containing the results of running the inference benchmark. Take into account the structure of the submission folder. The encrypted tarball should be computed in the following way (or in a way that is equivalent to):

  ```tar -cvzf <tarfile_name>.gz <submission_folder>
  openssl enc -e -aes256 -pass pass:<password> -pbkdf2 -in <tarfile_name>.gz -out <encrypted_tarfile_name>.gz```
  Here the <password> is a password of your choice that will be used to encrypt the tarball. After you upload the tarball, a submission_id will be generated and sent to you by email and will be displayed in the UI. The encrypted tarball will be stored in a GCS bucket. Make sure to store all the passwords you used, we will NOT store the passwords you used to encrypt the tarballs.
3. In the upper left corner of the interface, you will find a link to the submissions page. (Also notice that the image of the MLCommons logo is a link that takes you back to the main page). There you will be able to check the tarballs you uploaded using your Submitter ID and the submission_id.
  [Image](assets/images/run-submission-checker.png)
4. Enter the password you used to encrypt the tarball and click on the button "run submission checker". You will send a request to the server to check the results. The server will call a cloud function that does the following:
Decrypts (temporarily) your tarball using the password you provided in the appropriate field.
Untars/Unzips the file
Runs the script submission-checker.py on the results.
Sends you an email with the results that should look something like this:  [Image](assets/images/results.png)


5. (For Inference 2.0) After the submission deadline, we will contact you to ask you for a set of uploaded tarballs, the submission_ids and the passwords used to encrypt these you want to include in the final results. This set should satisfy the following conditions:
Every tarball should have been successfully checked (should have passed the submission checker)
Every tarball should have been uploaded before the deadline established (with exceptions according to the rules)
The set of tarballs should not have repeated systems to avoid conflicts between tarballs. That means 2 different selected tarballs should not have results for the same <SUT, model, software>. Here are 2 suggestions of how you might submit:
Put all of your results in the same tarball, run the verification test for this tarball and select it for the final results.
Put every system in a different tarball, run the verification test for all these tarballs and select them for the final results.



If the submitter not able to upload the tarball using submission UI (this is only a fall back option and is not the alternative)
- Share the MD5 hash (for the tarball on the git) with Results and Inference chairs.
