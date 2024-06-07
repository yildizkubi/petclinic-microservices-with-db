# Project 505: Microservices CI/CD Pipeline


# MSP-1

- Developer ların source kodlarını geliştirebilmeleri için manuel olarak bir Development Server hazırlandı. Server a docker, docker-compose, git ve java install edildi.


# MSP-2

- Proje için bir Github reposu oluşturuldu. Source kodlar Clarusway reposundan klonlandı ve oluşturduğumuz repo kendi repomuz haline getirildi.

- dev ve release branch leri oluşturuldu.


# MSP-3

- Maven komutları çalıştırıldı/denendi. Bunun için maven ın light versiyonu olan maven wrapper (mvnw) kullanıldı ve maven komutlarının sorunsuz bir şekilde çalıştığı görüldü.


# MSP-4

- ./mvnw clean package komutu, elimizde bir kayıt olması için "package-with-mvn-wrapper.sh" dosyası oluşturuldu ve repoya push landı.


# MSP-5

- İlk adımda manuel olarak oluşturulan Development Server ın terraform dosyaları hazırlandı ve şirkete daha sonra gelecek developerlar için kayıt altına alındı ve repoya push landı. 


# MSP-6

- Projeye yönelik olarak tüm microservice ler için Dockerfile lar hazırlandı ve repoya push landı.


# MSP-7

- Oluşturduğumuz Dockerfile lardan imajlar oluşturmak için gerekli olan komutların yer aldığı "build-dev-docker-images.sh" script dosyası hazırlandı ve repoya push landı.

# MSP-8

- Microservice uygulamasının çalışıp çalışmadığını görebilmek için Docker Compose dosyası (docker-compose-local.yml) hazırlandı ve script (test-local-deployment.sh) altına kaydedildi ve repoya push landı.

- Docker Compose çalıştırıldı ve uygulamanın çalıştığı görüldü.


# MSP-9

- CI/CD Jenkins Server oluşturuldu. Git, Docker, Docker Compose, AWS CLI v2, Python, Terraform, Ansible ve Boto3 install edildi."msp-9-jenkins-server-tf-template" repoya push landı.


# MSP-10

- CI/CD Jenkins Server ın konfigure işlemleri yapıldı.

- Github ta proje için oluşturduğumuz repo Jenkins Server a klonlandı.

- Github Integration, Docker, Docker Pipeline, Jacoco plugin leri install edildi.

# MSP-11

- Unit Test lerin çalıştırılabilmesi için Java Test dosyaları ilgili source kod  folder larda hazırlandı ve repoya pushlandı.

- Pom.xml de Code Coverage Report u görebilmek için Jacoco plugin i ile ilgili gerekli değişiklik yapıldı.

- "./mvnw test" komutu localde çalıştırılarak source kod ların test dosyaları çalıştırıldı ve unit test lerin çalıştığı görüldü.


# MSP-12

- Proje ile ilgili ilk Pipeline (petclinic-ci-job) Jenkins Server da oluşturuldu.

- Github Repo su için Webhook set edildi.

- Pipeline çalıştırıld ve Code Coverage Report görüldü.


# MSP-13

- Nightly Pipeline da çalıştırılacak olan Selenium Test dosyaları hazırlandı ve repoya push landı.


# MSP-14

- Nightly Pipeline a hazırlık amacıyla tüm adımların denemelerine başlandı.

- İlk olarak Jenkins'te bir Freestyle project oluşturularak bir ECR repo oluşturuldu.

- Oluşturulan ECR reponun komutları "create-ecr-docker-registry-for-dev.sh" script i olarak kaydedildi ve repoya pushlandı.

# MSP-15

- Nightly Pipeline ın çalışacağı cluster için 1 Master 2 Worker Server ı oluşturacak Terraform dosyaları hazırlandı ve repoya push landı.

- 3 server boş olarak oluşrulacak ve daha sonra Ansible ile bir Kubernetes Cluster haline getirilecek.


# MSP-16

- Nightly Pipeline a hazırlık amacıyla çeşitli komutların denemelerine devam edildi.

- Bu kapsamda "test-creating-qa-automation-infrastructure" isminde bir Freestyle project oluşturularak echo $PATH, whoami, python3 --version, pip3 --version, ansible --version, aws --version, terraform --version komutları çalıştırılarak ilgili toolların install edilip edilmediği denendi.

- Key-pair in başarılı bir şekilde oluşturulduğu görüldü.

- 1 Master, 2 Worker server ı oluşturan Terraform dosyası çalıştırıldı ve server ların oluştuğu görüldü.

- Oluşan server lara bağlanabildiğimizi denedik ve bağlanabildiğimi gördük.

- hosts.ini isminde bir inventory dosyası oluşturuldu ve repoya pushlandı.Oluşturulan hosts.ini inventory dosyası ile makinelere bağlanıp ping modülünün çalıştığı görüldü.

- "dev_stack_dynamic_inventory_aws_ec2.yaml" isminde dynamic inventory dosyası oluşturuldu ve repoya pushlandı.

- Dynamic inventory dosyası kullanılarak "dev_stack_dynamic_inventory_aws_ec2.yaml --graph" komutunun çalıştığı görüldü.

- Dynamic inventory dosyası kullanılarak server lara ping atılabildiği görüldü.

- Oluşturulan 1 Master 2 Worker server ın bir Kubernetes Cluster haline getirilebilmesi için "k8s_setup.yaml" dosyası oluşturuldu ve repoya pushlandı.

- "k8s_setup.yaml" çalıştırıldı ve 1 Master 2 Worker server ın Kubernetes Cluster haline geldiği görüldü.

- Daha sonra Kubernetes Cluster destroy edildi.

- Önceki adımda oluşturduğumuz key pair delete işlemi yapıldı.

- Yukarıdaki deneme adımları bir script (create-qa-automation-environment.sh) olarak kaydedildi ve repoya push landı.


# MSP17

- Kubernetes manifesto YAML file larımızın hazırlanabilmesi amacıyla ilk olarak "docker-compose.yml" dosyası oluşturuldu.

- "docker-compose.yml" dosyasından Kubernetes manifesto YAML file larının elde edilebilmesi amacıyla Kompose tool u install edildi.

- Helm paketlerinin oluşturulabilmesi için Helm install edildi.

- Helm paketleri oluşturuldu.

- "kompose convert -f docker-compose.yml -o petclinic_chart/templates" komutuyla docker-compose.yml dosyasından Kubernetes manifesto YAML file lar elde edildi.

- Microservice projesindeki service lerin belirli sırada çalışabilmesi sağlamak amacıyla manifesto YAML file larda gerekli değişiklikler (init container) yapıldı.

- Dynamic bir şekilde "values.yaml" dosyası elde edebilmek için "k8s/petclinic_chart/values-template.yaml" dosyası oluşturuldu.

- S3 bucket ın bir Helm repo olarak kullanılabilmesi amacıyla gerekli işlemler yapıldı. (bucket ın oluşturulması, helm s3 plugin in install edilmesi, index.yaml dosyasının oluşturulması, helm reponun localimize indirilmesi, chart.yaml dosyasında değişiklik yapılması, manifesto YAML file larının paketlenmesi ve S3 bucket a push lanması)

# MSP-18

- Nightly Pipeline nın hazırlanması işlemleri yapıldı.

- package-with-maven-container.sh, prepare-tags-ecr-for-dev-docker-images.sh, build-dev-docker-images-for-ecr.sh, push-dev-docker-images-to-ecr.sh script dosyaları hazırlandı ve repoya push landı ve bir Freestyle project job oluşturularak script lerin çalışıp çalışmadığı denendi.

- Uygulamanın deploy işleminin yapılabilmesi amacıyla "dev-petclinic-deploy-template" ansible playbook dosyası oluşturuldu.

- Selenium Testlerin denemesi yapmak amacıyla (dummy_selenium_test_headless.py) dosyası oluşturuldu.

- "dummy_selenium_test_headless.py" dosyasını çalıştırabilmek amacıyla "pb_run_dummy_selenium_job.yaml" ansible playbook oluşturuldu.

- "dummy_selenium_test_headless.py" yi çalıştıracak script dosyası (run_dummy_selenium_job.sh) oluşturuldu.

- "pb_run_dummy_selenium_job.yaml" playbook çalıştırıldı ve test in başarılı bir şekilde çalıştığı görüldü.

- Oluşturulan dosyalar repoya push landı.

- Yukarıdaki adımlarda localde denemesi yapılan dummy selenium testlerin Jenkinste oluşturulan bir Freestyle Projet (test-running-dummy-selenium-job) ile çalıştırılması sağlandı.

- Nightly Pipeline da çalışacak olan Selenium Testleri çalıştıracak ansible playbook dosyası (pb_run_selenium_jobs.yaml) oluşturuldu.

- Selenium Testler microservice uygulamamızın API-GATEWAY 30001 portundan yapılacağı için "test_owners_all_headless.py, test_owners_register_headless.py and test_veterinarians_headless.py" dosyalarında gerekli port değişiklikleri yapıldı.

- Selenium Testlerinin çalıştırılacağı script dosyası (run_selenium_jobs.sh) oluşturuldu.

- "jenkinsfile-petclinic-nightly" isimli Jenkinsfile oluşturuldu.

- Hazırlanan dosyalar Github repoya push landı.

- "petclinic-nightly" pipeline oluşturularak çalıştırıldı.


# MSP-19

- Weekly Pipeline hazırlıkları yapıldı.

- EKS cluster oluşturmak için cluster.yaml dosyası oluşturuldu ve repoya push landı.

- eksctl, kubectl install edildi.

- jenkins user a geçilerek "cluster.yaml" dosyası oluşturuldu. Çünkü cluster oluşturma komutunu "eksctl create cluster -f cluster.yaml" nerde girerseniz cluster ınızı yönetecek ./kube/config dosyası orda oluşur.

- jenkins user da "eksctl create cluster -f cluster.yaml" komutu girilerek cluster oluşturuldu.

- Cluster hazır olduktan sonra "ingress controller" install edildi.


# MSP-20

- "create-ecr-docker-registry-for-petclinic-qa" isimli bir Freestyle project oluşturarak ECR repo oluşturuldu.

- prepare-tags-ecr-for-qa-docker-images.sh, build-qa-docker-images-for-ecr.sh, push-qa-docker-images-to-ecr.sh, deploy_app_on_qa_environment.sh script dosyaları hazırlandı ve repoya push landı.


# MSP-21

- MSP-20 de oluşturulan script dosyalarını çalıştıracak "build-and-deploy-petclinic-on-qa-env-manually.sh" script dosyası hazırlandı.

- "build-and-deploy-petclinic-on-qa-env" isminde bir Freestyle project oluşturarak MSP-20 de oluşturulan script ler çalıştırıldı.

- "build-and-deploy-petclinic-on-qa-env-manually.sh" script dosyası Github repoya push landı.


# MSP-22

- Weekly Pipeline ı çalıştıracak "jenkinsfile-petclinic-weekly-qa" isimli Jenkinsfile oluşturuldu ve Github repoya push landı.

- "petclinic-weekly-qa" isimli bir Pipeline oluşturarak Weekly Pipeline çalıştırıldı.

- EKS Cluster silindi.


# MSP-23

- Rancher Server manuel olarak kurulması için hazırlıklara başlandı.

- "petclinic-rke-controlplane-policy.json", "petclinic-rke-etcd-worker-policy.json" policy leri oluşturuldu ve bu policy lerden "petclinic-rke-role" AWS console üzerinden oluşturuldu.

- Application Load Balancer ve Rancher Server için Security Group lar oluşturuldu ve port ayaralamaları yapıldı.

- Rancher Server için key-pair oluşturuldu.

- Rancher Servre için Ubuntu 22.04 bir instance launch edildi, Security Group ve Role bağlandı.

- Tag leme işlemleri yapıldı.

- Rancher Server a bağlanıp gerekli kurulum işlemleri yapıldı.

- Rancher Server Target Group oluşturuldu.

- Rancher Server a secure bir şekilde erişebilmek ve bir DNS ismi üzerinden bağlanabilmek amacıyla Application Load Balancer oluşturuldu ve ALB security group bağlandı.

- Port 80 in HTTPS Port 443 e redirect işlemi yapıldı.

- Route-53 te Rancher Server a erişebilmek için bir DNS kaydı oluşturuldu.

- Rancher Cluster ın oluşturulabilmesi için RKE tool u install edildi.

- Rancher Cluster ı oluşturabilmek için "rancher-cluster.yml" dosyası oluşturuldu.

- "rke up --config ./rancher-cluster.yml" komutuyla Rancher Cluster oluşturuldu.

- Rancher Cluster ı yönetebilmek için "./kube/config" dosyası oluşturuldu.

- Oluşturulan dosyalar Githun repoya push landı.


# MSP-24

- Rancher Cluster da Rancher App helm ile install edildi.

- Rancher Dashboard görüldü.


# MSP-25

- Nexus Server, Github repoda bulunan proje dosyasındaki terraform dosyalarından kuruldu.

- Nexus Server u kuran komutların bulunduğu dosya (nexus-server.tf) oluşturuldu ve Github repoya push landı.

- Nexus Server ın Proxy Repo ve Hoster Repo olarak kullanımı işlemleri yapıldı.


# MSP-26

- Staging Pipeline ı çalıştırmak için gerekli hazırlıklara başlandı.

- Rancher Server ın AWS ye erişebilmesini sağlamak amacıyla "Petclinic-AWS-Training-Account" isminde bir Cloud Credentials oluşturuldu.

- Rancher Server üzerinde 3 node dan oluşan bir Kubernetes Cluster oluşturuldu.

- Uygulamamızı deploy edebilmek amacıyla "petclinic-staging-ns" namespace oluşturuldu.

- "create-ecr-docker-registry-for-petclinic-staging" isminde bir Freestyle Project oluşturarak Staging için bir ECR repo oluşturuldu.

- prepare-tags-ecr-for-staging-docker-images.sh, build-staging-docker-images-for-ecr.sh, push-staging-docker-images-to-ecr.sh scriptleri oluşturuldu.

- Rancher Server üzerinden oluşturduğumuz Kubernetes cluster ı Jenkins Server üzerinden yönetebilmek amacıyla Rancher CLI install edildi.

- Jenkins Server üzerinden Rancher Server da oluşturduğumuz Cluster a uygulamayı deploy edebilmek amacıyla Rancher Serverda API Key i oluşturarak Jenkins Server a tanıtma işlemleri yapıldı.

- "jenkinsfile-petclinic-staging" isimli Jenkinsfile hazırlandı ve oluşturulan tüm dosyalar Github repoya pushlandı.

- Uygulamamıza bir DNS ismi üzerinden erişebilmek için Route-53 te bir A record oluşturuldu.

- Jenkins Server da "petclinic-staging" isimli bir Pipeline oluşturarak Staging Pipeline çalıştırıldı ve uygulama görüldü.


# MSP-27

# MSP-28

# MSP-29