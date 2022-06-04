# DevOps-project-1

# The goal of this project is to use terraforming to create a Linode instance.
    
# Make a Terraform project directory in your home directory and then navigate to it: 

mkdir ~/terraform 
cd ~/terraform 

# install terraform  
sudo apt update  
sudo apt upgrade 

# Download the Terraform download file from Terraform's website, making sure to install the most recent version available.
# The 64-bit Linux .zip archive  wget https://releases.hashicorp.com/
terraform/1.1.9/
terraform_1.1.9_linux_amd64.zip   

# Import the HashiCorp Security GPG key 34365D9472D7468F 
gpg --recv-keys 34365D9472D7468F

# Verify the checksum file’s GPG signature:  
gpg --verify terraform*.sig terraform*SHA256SUMS 

# Verify the .zip archive’s checksum:  sha256sum -c terraform*SHA256SUMS 2>&1 | grep OK  
terraform_1.1.9_linux_amd64.zip: OK  

# Configure the Terraform Environment  Unzip terraform_*_linux_amd64.zip to your ~/terraform directory:   
unzip terraform_*_linux_amd64.zip  
# Edit your ~./profile to include the ~/terraform directory in your PATH. Then, reload the Bash profile:  

echo 'export PATH="$PATH:$HOME/
terraform"' >> ~/.profile 
source ~/.profile  

# To test Terraform's ability to operate, simply call it without any options or arguments:
terraform   

# Building the linode instance
# create a main.tf file in your terraform directory/folder 
nano main.tf   
# paste the following  
terraform {   
  required_providers {      
    linode = {      
      source = "linode/linode"       
      version = "1.27.1"     
    }   
  }  
}   
provider "linode" {    
  token = "YOUR_LINODE_API_TOKEN"  
}    

resource "linode_instance" "terraform-web"
{  
        label = "ojoabodunde"         
        group = "Terraform"         
        region = "Dallas, TX"       
        type = "g6-standard-1"         
        authorized_keys = [ "YOUR_PUBLIC_SSH_KEY" ]        
        root_pass = "YOUR_ROOT_PASSWORD"  
} 
# Fill in your Linode API token, public SSH key, and desired root password where indicated. Additionally, replace the Linode provider version to the latest as well as the label: 

# Initialize the Terraform configuration: 
terraform init  

# Note  
# If an error occurs, run the command again in debug mode:
TF_LOG=debug terraform init  

# Run Terraform’s plan command:  
terraform plan  

# Next run  
terraform apply   

You'll be asked to confirm your decision. 
Yes, please, and hit Enter:

# Go to the Linode Manager page. 

Your Linode instance should now be visible in your account settings.

I hope you had fun terraforming. Best wishes.
