# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Ubuntu 20.04 LTS (Focal)
  config.vm.box = "ubuntu/focal64"

  # Forward Confluence port 1990
  config.vm.network "forwarded_port", guest: 1990, host: 1990

  # Desktop / GUI optimized configuration
  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.cpus = 2
    vb.memory = "4096"
    vb.customize ["modifyvm", :id, "--accelerate3d", "on"]
    vb.customize ["modifyvm", :id, "--vram", "128"]
  end

  # Provisioning (JVM, Atlassian SDK, Fonts, Ubuntu Desktop)
  config.vm.provision "shell", inline: <<-SHELL
    APT_ATLASSIAN_SDK_KEY="https://packages.atlassian.com/api/gpg/key/public"
    APT_ATLASSIAN_SDK_REPO="deb https://packages.atlassian.com/debian/atlassian-sdk-deb stable contrib"
    APT_ADOPTOPENJDK_KEY="https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public"
    APT_ADOPTOPENJDK_REPO="https://adoptopenjdk.jfrog.io/adoptopenjdk/deb"
    GOOGLE_CHROME="https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb"
    wget -qO - "${APT_ADOPTOPENJDK_KEY}" \
      | apt-key add -
    add-apt-repository --yes "${APT_ADOPTOPENJDK_REPO}"
    # Atlassian SDK repository
    wget -qO - "${APT_ATLASSIAN_SDK_KEY}" \
      | apt-key add -
    add-apt-repository --yes "${APT_ATLASSIAN_SDK_REPO}"
    # Accept Microsoft EULA
    echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true \
      | debconf-set-selections
    # Install packages
    apt-get update -q && apt-get install -yyq \
      adoptopenjdk-11-hotspot \
      atlassian-plugin-sdk \
      ttf-mscorefonts-installer \
      ubuntu-desktop
    # Start desktop
    systemctl isolate graphical
  SHELL
end
