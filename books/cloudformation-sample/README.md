# 1 開発環境の構築

## 環境の確認

```
aws --version
aws cloudformation help
aws cloudformation describe-stacks help
```

## aws cli のためのコマンド補完設定

```
echo "complete -C '/usr/local/bin/aws_completer' aws" >> ~/.bashrc
source ~/.bashrc
```

# 2 VPCの作成
## CloudFormationの実行コマンド

### validate(検証)

```
aws cloudformation validate-template --template-body file://01_vpc.yaml
```

### create

```
aws cloudformation create-stack --stack-name handson-cfn --template-body file://01_vpc.yaml
```

### update

```
aws cloudformation update-stack --stack-name handson-cfn --template-body file://01_vpc.yaml
```

# 3 EC2の作成

## CloudFormationの実行コマンド

### validate

```
aws cloudformation validate-template --template-body file://02_ec2.yaml
```

### create

```
aws cloudformation create-stack --stack-name handson-cfn-ec2 --template-body file://02_ec2.yaml
```

### update

```
aws cloudformation update-stack --stack-name handson-cfn-ec2 --template-body file://02_ec2.yaml
```

# 4 RDS・ELBの作成

## CloudFormationの実行コマンド

### validate

```
aws cloudformation validate-template --template-body file://03_rds.yaml
aws cloudformation validate-template --template-body file://04_elb.yaml
```

### create

```
aws cloudformation create-stack --stack-name handson-cfn-rds --template-body file://03_rds.yaml
aws cloudformation create-stack --stack-name handson-cfn-elb --template-body file://04_elb.yaml
```

DBName:
wordpress
DBUser:dbmaster
DBPassword: H&ppyHands0n
