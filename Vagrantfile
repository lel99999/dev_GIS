Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = "1024"
    v.cpus = 2
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "70"]
  end
# config.trigger.after :up do |trigger|
#   run "subscription-manager register --username <username> --password <password> --auto-attach
#   trigger.name = "After-Up Trigger ..."
#   trigger.info = "Trigger Execution ..."
#   trigger.run = { path:"subscription-manager register --username <username> --password <password> --auto-attach"}
# end

  config.vm.define "RTidyverseRH7" do |RTidyverseRH7|
    RTidyverseRH7.vm.box = "clouddood/RH7.5_baserepo"
    RTidyverseRH7.vm.hostname = "RTidyverseRH7"
    RTidyverseRH7.vm.network "private_network", ip: "192.168.60.147"
    RTidyverseRH7.vm.provision "shell", :inline => "sudo echo '192.168.60.147 RTidyverseRH7.local RTidyverseRH7' >> /etc/hosts"


##  Use Main / Update in Vagrant provision command ### $vagrant provision --provision-with shell/main/update

    # Default 
    # Main
    RTidyverseRH7.vm.provision "main", type: "ansible" do |ansible|
#     ansible.playbook = "deploy_RTidyverseRH7.yml"
#     ansible.playbook = "deploy_RTidyverseTest.yml"
      ansible.playbook = "deploy_RTidyverseTest.yml"
      ansible.inventory_path = "vagrant_hosts"
      #ansible.tags = ansible_tags
      #ansible.verbose = ansible_verbosity
      #ansible.extra_vars = ansible_extra_vars
      #ansible.limit = ansible_limit
    end
    # Update
    RTidyverseRH7.vm.provision "update", type: "ansible" do |ansible|
      ansible.playbook = "deploy_RTidyversePatchRH7.yml"
      ansible.inventory_path = "vagrant_hosts"
      #ansible.tags = ansible_tags
      #ansible.verbose = ansible_verbosity
      #ansible.extra_vars = ansible_extra_vars
      #ansible.limit = ansible_limit
    end
  end
# config.trigger.before :destroy do |trigger|
#   run "rm -Rf /tmp/abc/*"
    # subscription-manager remove --all
    # subscription-manager unregister
    # subscription-manager clean
#   trigger.name = "Destroy Trigger ..."
#   trigger.info = "Destroy Trigger Execution ..."
#   trigger.run = { path: "subscription-manager remove --all"}
#   trigger.run = { path: "subscription-manager unregister"}
#   trigger.run = { path: "subscription-manager clean"}
# end
end
