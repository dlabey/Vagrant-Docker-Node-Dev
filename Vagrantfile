ENV['VAGRANT_DEFAULT_PROVIDER'] = "docker"
DOCKER_HOST_NAME = "host"
DOCKER_HOST_VAGRANTFILE = "Vagrantfile.host"

Vagrant.configure("2") do |config|

  # Setup a Node container
  config.vm.define "node" do |node|

    # Configure the Node container
    node.vm.provider "docker" do |docker|
      docker.name = "node"
      docker.remains_running = true
      docker.vagrant_machine = "#{DOCKER_HOST_NAME}"
      docker.vagrant_vagrantfile = "#{DOCKER_HOST_VAGRANTFILE}"
      docker.image = "node"
      docker.volumes = ["/mnt/node"]
      docker.ports = ["3000:3000"]
      docker.has_ssh = true
    end

  end

  # Setup a Postgres container
  config.vm.define "postgres" do |postgres|

    # Configure the Postgres container
    postgres.vm.provider "docker" do |docker|
      docker.name = "postgres"
      docker.remains_running = true
      docker.vagrant_machine = "#{DOCKER_HOST_NAME}"
      docker.vagrant_vagrantfile = "#{DOCKER_HOST_VAGRANTFILE}"
      docker.image = "postgres"
      docker.volumes = ["/mnt/postgres:/data"]
      docker.ports = ["5432:5432"]
      docker.has_ssh = true
      docker.link("node:node")
      docker.env = {
        POSTGRES_USER: "root",
        POSTGRES_PASSWORD: "root"
      }
    end

  end

  # Setup a Redis container
  config.vm.define "redis" do |redis|

    # Configure the Redis container
    redis.vm.provider "docker" do |docker|
      docker.name = "redis"
      docker.remains_running = true
      docker.vagrant_machine = "#{DOCKER_HOST_NAME}"
      docker.vagrant_vagrantfile = "#{DOCKER_HOST_VAGRANTFILE}"
      docker.image = "redis"
      docker.volumes = ["/mnt/redis:/data"]
      docker.ports = ["6379:6379"]
      docker.has_ssh = true
      docker.link("node:node")
    end

  end

end
