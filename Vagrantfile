Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.synced_folder "./www", "/var/www",
    :owner => "vagrant",
    :group => "vagrant",
    :mount_options => ['dmode=775','fmode=664']

  config.vm.provision "shell", inline: <<-EOT
    sed -i 's/^SELINUX=.*$/SELINUX=disabled/g' /etc/selinux/config

    yum update

    yum install epel-release -y

    # Install Apache
    yum install httpd -y
    sed -i 's/^User .*$/User vagrant/g' /etc/httpd/conf/httpd.conf
    sed -i 's/^Group .*$/Group vagrant/g' /etc/httpd/conf/httpd.conf

    # Install MariaDB
    yum install mariadb-server -y
    if ! grep skip-grant-tables /etc/my.cnf >/dev/null; then
      echo skip-grant-tables >> /etc/my.cnf
    fi
    systemctl start mariadb.service
    mysql -u root -e "CREATE DATABASE IF NOT EXISTS wordpress"
    systemctl stop mariadb.service

    # Install PHP
    rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
    yum install --enablerepo=remi,remi-php71 php php-devel php-mbstring php-mysqlnd php-pdo php-gd php-xml php-mcrypt -y 
  EOT

  config.vm.provision "shell", run: "always", inline: "systemctl start httpd.service"
  config.vm.provision "shell", run: "always", inline: "systemctl start mariadb.service"
end
