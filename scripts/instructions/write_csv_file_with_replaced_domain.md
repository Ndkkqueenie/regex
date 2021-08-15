Write a CSV file with replaced domain from main
In this section, we're going to call the above defined functions: contains_domain() and replace_domain from the main(). This will allow us to find the old domain email address, replace it with the newer one, and write the updated list to a CSV file in the data directory.

In the previous sections, you might have seen variables named old_domain and new_domain, which are passed as parameters to the functions. Let's declare them here within main().

```
  old_domain, new_domain = 'abc.edu', 'xyz.edu'
```

Now store the path of the list user_emails.csv in the variable csv_file_location. Also, give a file path for the resulting updated list within the variable report_file. This updated list should be generated within the data directory.

```
  csv_file_location = '<csv-file-location>'
  report_file =  '<data-directory>' + '/updated_user_emails.csv'
```

Replace <csv_file_location> by the path to the user_emails.csv. <csv_file_location> is similar to the path /home/<username>/data/user_emails.csv. For variable report_file, replace <data_directory> by the path to /data directory. <data_directory> is similar to the path /home/<username>/data. Replace <username> with the one mentioned in the Connection Details Panel on the left-hand side.

Then, initialize an empty list where you will store the user email addresses. This is then passed to the function contains_domain, where a regular expression is used to match them and finally replace the domains using the replace_domain function.

Next, initialize the two different lists, old_domain_email_list and new_domain_email_list. The old_domain_email_list will contain all the email addresses with the old domain that the regex would match within the function contains_domain. Since the function contains_domain takes in email address passed as parameter, we will iterate over the user_email_list to pass email addresses one by one. For every matched email address, we will append it to the list old_domain_email_list.

```
  user_email_list = []
  old_domain_email_list = []
  new_domain_email_list = []
```

The CSV module imported earlier implements classes to read and write tabular data in CSV format. The CSV library provides functionality to both read from and write to CSV files. In this case, we are first going to read data from the list (which is a CSV file). The data is read from the user_emails.csv file and passed to the user_data_list. So the user_data_list now contains the same information as that present in user_emails.csv file. While we do this, we will also add all the email addresses into the user_email_list that we initialized in the previous step.

```
  with open(csv_file_location, 'r') as f:
    user_data_list = list(csv.reader(f))
    user_email_list = [data[1].strip() for data in user_data_list[1:]]
```

The list old_domain_email_list should contain all the email addresses with the old domain. This will be checked by the function contains_domain. The function replace_domain will then take in the email addresses (with old domain) and replace them with the new domains.

```
    for email_address in user_email_list:
      if contains_domain(email_address, old_domain):
        old_domain_email_list.append(email_address)
        replaced_email = replace_domain(email_address, old_domain, new_domain)
        new_domain_email_list.append(replaced_email)
```

Now, let's define the headers for our output file through the user_data_list, which contains all the data read from user_emails.csv file.

```
    email_key = ' ' + 'Email Address'
    email_index = user_data_list[0].index(email_key)
```

Next, replace the email addresses within the user_data_list (which initially had all the user names and respective email addresses read from the user_emails.csv file) by iterating over the new_domain_email_list, and replacing the corresponding values in user_data_list.

Finally, close the file using the close() method. A closed file no longer be read or written. It is good practice to use the close() method to close a file.

```
    for user in user_data_list[1:]:
      for old_domain, new_domain in zip(old_domain_email_list, new_domain_email_list):
        if user[email_index] == ' ' + old_domain:
          user[email_index] = ' ' + new_domain
    f.close()
```
Now write the list to an output file, which we declared at the beginning of the script within the variable report_file.

```
  with open(report_file, 'w+') as output_file:
    writer = csv.writer(output_file)
    writer.writerows(user_data_list)
    output_file.close()
```
Finally, call the main() method.

```
main()
```