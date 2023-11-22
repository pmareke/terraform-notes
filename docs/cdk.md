# [CDK for Terraform](https://developer.hashicorp.com/terraform/cdktf)

- Cloud Development Kit for Terraform (CDKTF) allows you to use familiar programming languages to define and provision infrastructure.

## How does CDK for Terraform work?

- Create an Application using either a built-in or a custom template to scaffold a project in your chosen language.
- Define Infrastructure, CDKTF automatically extracts the schema from Terraform providers and modules to generate the necessary classes for your application.
- Deploy using cdktf CLI commands to provision infrastructure with Terraform or synthesize your code into a configuration file.

## Install CDKTF

- `npm install --global cdktf-cli@latest`
- `cdktf init --template=python --providers=kreuzwerker/dock--local`

```python
#!/usr/bin/env python

from constructs import Construct
from cdktf import App, TerraformStack
from cdktf_cdktf_provider_docker.image import Image
from cdktf_cdktf_provider_docker.container import Container
from cdktf_cdktf_provider_docker.provider import DockerProvider


class MyStack(TerraformStack):
    def __init__(self, scope: Construct, ns: str):
        super().__init__(scope, ns)

        DockerProvider(self, 'docker')

        docker_image = Image(self, 'nginxImage',
            name='nginx:latest',
            keep_locally=False)

        Container(self, 'nginxContainer',
            name='tutorial',
            image=docker_image.name,
            ports=[{
                'internal': 80,
                'external': 8000
            }])


app = App()
MyStack(app, "learn-cdktf-docker")

app.synth()
```
The CDKTF code above is equivalent to the following HCL configuration:

```terraform
resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.name
  name  = "tutorial"
  ports {
    internal = 80
    external = 8000
  }

```

## Build AWS infrastructure with CDK for Terraform

- `cdktf init --template="python" --providers="aws@~>4.0"`

```python
#!/usr/bin/env python
from constructs import Construct
from cdktf import App, NamedRemoteWorkspace, TerraformStack, TerraformOutput, RemoteBackend
from cdktf_cdktf_provider_aws.provider import AwsProvider
from cdktf_cdktf_provider_aws.instance import Instance


class MyStack(TerraformStack):
    def __init__(self, scope: Construct, ns: str):
        super().__init__(scope, ns)

        AwsProvider(self, "AWS", region="us-west-1")

        instance = Instance(self, "compute",
                            ami="ami-01456a894f71116f2",
                            instance_type="t2.micro",
                            )

        TerraformOutput(self, "public_ip",
                        value=instance.public_ip,
                        )


app = App()
stack = MyStack(app, "aws_instance")

RemoteBackend(stack,
              hostname='app.terraform.io',
              organization='<YOUR_ORG>',
              workspaces=NamedRemoteWorkspace('learn-cdktf')
              )

app.synth()
```
