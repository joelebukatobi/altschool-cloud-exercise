## Month Two

### Week Four / Exercise Eight

In week four we talked about setting up environments using ansible. What is ansible?

Well according to [opensource.com](https://opensource.com/resources/what-ansible)

Ansible is a software tool that provides simple but powerful automation for cross-platform computer support. It is primarily intended for IT professionals, who use it for application deployment, updates on workstations and servers, cloud provisioning, configuration management, intra-service orchestration, and nearly anything a systems administrator does on a weekly or daily basis. Ansible doesn't depend on agent software and has no additional security infrastructure, so it's easy to deploy.

For this task we were asked to

- Create an Ansible Playbook to setup a server with Apache
- The server should be set to the Africa/Lagos Timezone
- Host an index.php file with the following content, as the main file on the server:

```
<?php
date_default_timezone_set('Africa/Lagos');
echo date("F d, Y h:i:s A e", time());
?>
```

#### Submission Documents

Screenshot of the rendered page
![alt](/month-two/week-four/exercise-eight/index-screenshot.png)

---

The output of `systemctl status apache2`
![alt](/month-two/week-four/exercise-eight/apache2-status.png)
