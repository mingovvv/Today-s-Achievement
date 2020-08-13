Provider
```
    provider "aws" {
  access_key = " 키 입력 "
  secret_key = "키 입력"
  region = "ap-northeast-2"
}
```
Terraform을 실행하기 위해서는 IAM에 있는 Access Key와 Secret Key를 입력해야 한다.
Terraform을 사용하기 위해서는 *.tf 파일이 위치한 폴더에서 아래 명령을 입력한다.

terraform init
 - Terraform 버전관리 및 문법 검사

terraform plan / terraform apply
 - Terraform 적용

terraform destroy
 - 이미 전개된 자원 삭제


#### 기본개념
Resource는 Terraform에서 가장 중요한 요소이며, 리소스는 네트워크, 인스턴스, S3와 같은 스토리지, DNS 레코드 등 Infra를 구성하는 객체들이다.
기본 구조는 Resoruce블록과 Argument 구조로 가진다. Resource 블록안에는 자원의 속성을 설정하기 위한 Argument들이 있다.
로컬이름은 같은 종류의 자원들을 서로 식별하기 위한 목적으로 사용된다.
 

```
VPC
resource "aws_vpc" "main" {
  cidr_block       = "10.0.0.0/16"
  instance_tenancy = "default"

  tags = {
    Name = "main"
  }
}
```
```
Subnet
resource "aws_subnet" "public_subnet" {
  vpc_id     = aws_vpc.public_subnet.id
  cidr_block = "10.0.1.0/24"

  tags = {
    Name = "Main"
  }
}
resource "aws_subnet" "private_subnet" {
  vpc_id     = aws_vpc.private_subnet.id
  cidr_block = "10.0.1.0/24"

  tags = {
    Name = "Main"
  }
}
``` 

```
Internet Gateway
resource "aws_internet_gateway" "gw" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "main"
  }
}
``` 
```
Route
resource "aws_route" "r" {
  route_table_id            = "rtb-4fbb3ac4"
  destination_cidr_block    = "10.0.1.0/22"
  vpc_peering_connection_id = "pcx-45ff3dc1"
  depends_on                = [aws_route_table.testing]
}
 ```
```
Route Table
resource "aws_route_table" "r" {
  vpc_id = aws_vpc.default.id

  route {
    cidr_block = "10.0.1.0/24"
    gateway_id = aws_internet_gateway.main.id
  }

  tags = {
    Name = "main"
  }
}
 ```
```
Route Table Association
resource "aws_route_table_association" "a" {
  subnet_id      = aws_subnet.foo.id
  route_table_id = aws_route_table.bar.id
}

resource "aws_route_table_association" "b" {
  gateway_id     = aws_internet_gateway.foo.id
  route_table_id = aws_route_table.bar.id
}
 ```
```
Security Group
resource "aws_security_group" "allow_tls" {
  name        = "allow_tls"
  description = "Allow TLS inbound traffic"
  vpc_id      = "${aws_vpc.main.id}"

  ingress {
    description = "TLS from VPC"
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = [aws_vpc.main.cidr_block]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "allow_tls"
  }
}
 ```
```
Security Group Rule
resource "aws_security_group_rule" "example" {
  type              = "ingress"
  from_port         = 0
  to_port           = 65535
  protocol          = "tcp"
  cidr_blocks       = [aws_vpc.example.cidr_block]
  security_group_id = "sg-123456"
}

resource "aws_security_group_rule" "allow_all" {
  type              = "egress"
  to_port           = 0
  protocol          = "-1"
  prefix_list_ids   = [aws_vpc_endpoint.my_endpoint.prefix_list_id]
  from_port         = 0
  security_group_id = "sg-123456"
}
 ```
```
반복문 : For-Each, For-Loop
IAM Role에 정책을 연결하는 코드 - 반복문 적용 전

locals {
  lambda_backend_policy_arns = [
    "arn:aws:iam::aws:policy/AmazonRDSFullAccess",
    "arn:aws:iam::aws:policy/CloudWatchFullAccess",
    "arn:aws:iam::aws:policy/AmazonDynamoDBFullAccess",
  ]
}
```
```
resource "aws_iam_role_policy_attachment" "attach" {
  count = "\${length(local.lambda_backend_policy_arns)}"

  role = "${aws_iam_role.lambda_backend.name}"
  policy_arn = "${local.lambda_backend_arns[count.index]}"
}
 
```
IAM Role에 정책을 연결하는 코드 - 반복문 적용 후
```
variable "subnet_numbers" {
  default = {
    "ap-northeast-2a" = 1
    "ap-northeast-2b" = 2
    "ap-northeast-2c" = 3
  }
}

resource "aws_subnet" "example" {
  for_each = var.subnet_numbers

  vpc_id = aws_vpc.example.id
  availability_zone = each.key
  cidr_block = cidrsubset(
    aws_vpc.example.cidr_block, each.value
  )
}
```