# Welcome to AWS Code Commit
You can use the AWS Management Console and upload, add, or edit a file to a repository directly from the AWS CodeCommit console. This is a quick way to make a change. However, if you want to work with multiple files, files across branches, and so on, consider setting up your local computer to work with repositories. In this demo, we will learn how to setup AWS Code Commit using SSH and IAM roles.

![Set Up SSH Connections to AWS CodeCommit Repositories](https://raw.githubusercontent.com/miztiik/setup-aws-code-commit/master/images/SSH%20Connections%20to%20AWS%20CodeCommit%20Repositories.png)

#### Follow this article in [Youtube](https://www.youtube.com/watch?v=OHXDPDc1qEE&list=PLxzKY3wu0_FKok5gI1v4g4S-g-PLaW9YD&index=20)

## Set Up SSH Connections to AWS CodeCommit Repositories

_**Note:** This is for Linux/Mac users._
0. ### Create IAM Users/Groups

    It is better to have a seperate groups(say `Devs`) and add your users to that group.

    Add Group Permission - Managed Policy - `AWSCodeCommitFullAccess`

1. ### Create SSH Keys
    ```sh
    # Create the `.ssh` directory if it isn't there already
    # mkdir -p $HOME/.ssh
    cd $HOME/.ssh
    ssh-keygen
    # [here just create the name codecommit_rsa and leave all fields blank *just click enter*]
    cat codecommit_rsa.pub  
    ```
1. ### Associate Your Public Key with Your IAM User
    - Now we need to enter our `codecommit_rsa.pub` into AWS IAM. 
    - Copy the SSH key ID (for example, `APKAEIBAERJR2EXAMPLE`)
1. ### Add AWS CodeCommit to Your SSH Configuration
    ```sh
    cd $HOME/.ssh
    touch config
    chmod 600 config
    cat > $HOME/.ssh/config << "EOF"
    Host git-codecommit.*.amazonaws.com
      User YOUR_SSH_KEY_ID_FROM_IAM
      IdentityFile ~/.ssh/codecommit_rsa
    EOF
    ```

1. ### Test your SSH configuration:
    ```sh
    ssh git-codecommit.us-east-1.amazonaws.com
    ```

You should see something like this,
> You have successfully authenticated over SSH. You can use Git to interact with AWS CodeCommit. Interactive shells are not supported.Connection to git-codecommit.us-east-1.amazonaws.com closed by remote host.