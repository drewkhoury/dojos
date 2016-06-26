CloudFormation 101 :: Setup
===========================

# Setup Instructions

If you'd like to host the exercises for others to run, we've provided a CloudFormation template that creates the required VPC, Subnet, Security Group and Jumpbox.

Create the supporting stack by doing the following:
- Log into AWS https://signin.aws.amazon.com/console/
- Selecting `Servces > CloudFormation > Create Stack`
- Choose the template `./scr/setup/cf101-vpc.template` (supplied in this repo)

Continue with the wizard, filling in values as required. Most options are straight forward but here are some hints:
- Give your stack a name (e.g cf101)
- Supply a valid AWS KeyName (a Public key you've already uploaded to AWS)
- Continue with the defaults for everything else

This will create a VPC (an isolated network for us to play in) and Jumpbox (a virtual machine that we'll use as an entry point to login to other machines via ssh). This is a common pattern for AWS and other networks.

![Setup](setup.png "Setup")

If you're intended on having others follow the exercises you'll want to manage ssh users and keys on the jumpbox. There's a script `./src/setup/create_user.sh` that has been supplied to handle this for you if you update the `S3_URL` variable to point to an S3 Bucket with the public keys. You can then run this script on the Jumpbox. (Note: We may want to automate this a bit further in CF with s3 bucket, add an iam role, and copy the script to the ec2 run as a cronjob)

If you just want to provision users manually, here is an example of how to configure a user for ssh access:

```
# config
USERNAME=foo

# create user
sudo /usr/sbin/useradd -m $USERNAME

# ssh config :: .ssh
sudo mkdir /home/$USERNAME/.ssh
sudo /bin/chown $USERNAME:$USERNAME /home/$USERNAME/.ssh
sudo /bin/chmod 700 /home/$USERNAME/.ssh/

# ssh config :: authorized_keys
touch /home/$USERNAME/.ssh/authorized_keys
sudo /bin/chmod 600 /home/$USERNAME/.ssh/authorized_keys
sudo /bin/chown $USERNAME:$USERNAME /home/$USERNAME/.ssh/authorized_keys

# add public key to authorized_keys so the user can ssh
cat <<EOF | sudo tee /home/$USERNAME/.ssh/authorized_keys > /dev/null
-----BEGIN RSA PRIVATE KEY-----
public_key_content_removed_for_this_example
public_key_content_removed_for_this_example
public_key_content_removed_for_this_example
public_key_content_removed_for_this_example
-----END RSA PRIVATE KEY-----
EOF
```