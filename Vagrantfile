# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.env.enable
  config.vm.box = "hashicorp/bionic64"

  config.vm.provision :shell do |s|
    s.privileged = true
    s.inline = <<-SHELL
      # Install AWS Command Line Interface (CLI)
      sudo apt-get update -y
      sudo apt-get install -y awscli

      # Configure AWS CLI with your credentials and default region
      su - vagrant -c "aws configure set aws_access_key_id '${AWS_ACCESS_KEY_ID}'"
      su - vagrant -c "aws configure set aws_secret_access_key '${AWS_SECRET_ACCESS_KEY}'"
      su - vagrant -c "aws configure set region '${AWS_DEFAULT_REGION:-us-east-1}'"
    SHELL
    
    s.env = {
      "AWS_ACCESS_KEY_ID" => ENV['AWS_ACCESS_KEY_ID'],
      "AWS_SECRET_ACCESS_KEY" => ENV['AWS_SECRET_ACCESS_KEY'],
      "AWS_DEFAULT_REGION" => ENV['AWS_DEFAULT_REGION'],

      "DEBIAN_FRONTEND" => "noninteractive" # To avoid any interactive prompts during package installation
    }
  end
end
