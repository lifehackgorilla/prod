---
title: "【期間限定：無料公開】イラストで速攻理解IT入門AWS 全編"
emoji: "☁️"
type: "tech"
topics: ["aws", "初心者", "クラウド", "インフラ"]
published: false
---

[後編へ進む](/articles/aws-study-guide-02)

## このシリーズについて

この記事は「【期間限定：無料公開】イラストで速攻理解IT入門AWS」の前編です。はじめに〜第15章までを扱います。

- [前編: はじめに〜第15章](/articles/aws-study-guide-01)
- [後編: 第16章〜最終まとめ](/articles/aws-study-guide-02)

![絶対にわかるAWS 学習資料](/images/aws-study/fig_001_aws.png)


# はじめに

![はじめに](/images/aws-study/fig_002_aws_learning.png)
この記事について
初心者の方にも無理なく理解していただけるよう、学習の基礎となる内容をわかりやすく図で解説しています。
これからの学びを支える一助になれば幸いです。

著者：ライフハックゴリラ（x.com ⇒ @LifeHackGorilla）
経歴：システムエンジニア歴5年以上

企業でAI担当をしています。
Kindleで複数の書籍を出版しています。Xをフォローしていただくと見逃さずにすむかもしれません。

X ⇒ https://x.com/LifeHackGorilla

システムエンジニアとしてAWSを基礎から実務レベルまで理解するための学習資料です。AWSはサービス数が多いため、最初からすべてのサービスを暗記しようとすると挫折しやすくなります。大切なのは、**サービス名を覚えることではなく、何を解決するためのサービスなのかを理解すること**です。

AWSを学ぶときは、クラウドの考え方、アカウントとセキュリティ、ネットワーク、コンピューティング、ストレージ、データベース、公開構成、監視、コスト、IaC、設計評価の順に進めると理解しやすくなります。

**AWSは、サーバーを借りる場所ではありません。アプリケーションを安全に、止まりにくく、拡張しやすく、運用しやすく作るための部品が集まったクラウド基盤です。**

---

# 第1章 AWSとクラウドの全体像

![第1章 AWSとクラウドの全体像](/images/aws-study/fig_003_aws.png)


## 1.1 AWSとは何か

![1.1 AWSとは何か](/images/aws-study/fig_042_aws.png)


AWSはAmazon Web Servicesの略です。サーバー、ストレージ、データベース、ネットワーク、セキュリティ、AI、分析、開発者ツールなどをインターネット経由で利用できるクラウドサービス群です。

従来は、システムを作るために物理サーバーを購入し、データセンターへ設置し、ネットワーク機器、電源、冷却、保守まで考える必要がありました。AWSでは、これらの多くをAWSが用意してくれるため、利用者は必要なリソースを必要な分だけ作成できます。

**AWSの本質は、ITインフラをコードや設定で素早く作成・変更・削除できることです。**これにより、システム開発のスピードが上がり、初期投資を抑えやすくなります。

## 1.2 クラウドコンピューティングとは何か

![1.2 クラウドコンピューティングとは何か](/images/aws-study/fig_043_aws_learning.png)


クラウドコンピューティングとは、サーバーやストレージなどのITリソースを、インターネット経由で必要なときに利用する仕組みです。自社で機器を買って持つのではなく、クラウド事業者が用意した巨大な基盤を利用します。

クラウドは、必要なときにすぐ使え、使った分に応じて料金が発生し、台数や容量を増減しやすいことが特徴です。たとえるなら、オンプレミスは自分で発電機を買って電気を作る方式、クラウドは電力会社から必要な分だけ電気を使う方式に近いです。

| 観点 | オンプレミス | AWSクラウド |
|---|---|---|
| 初期投資 | 機器購入が必要 | 小さく始めやすい |
| 拡張 | 調達に時間がかかる | 数分で増減しやすい |
| 管理範囲 | 物理機器も管理 | 物理基盤はAWSが管理 |
| コスト | 固定費が中心 | 従量課金が中心 |
| 変更速度 | 手続きが重い | APIやIaCで変更しやすい |

## 1.3 IaaS、PaaS、SaaS

![1.3 IaaS、PaaS、SaaS](/images/aws-study/fig_044_aws_learning.png)


IaaSはInfrastructure as a Serviceの略で、仮想サーバーやネットワークなどの基盤を提供する形態です。Amazon EC2は代表的なIaaSです。OSやミドルウェアの管理は利用者が行います。

PaaSはPlatform as a Serviceの略で、アプリケーションを動かすための実行環境を提供する形態です。AWS LambdaやAWS Elastic Beanstalkなどが近い考え方です。サーバー管理の負担を減らせます。

SaaSはSoftware as a Serviceの略で、完成したアプリケーションをサービスとして利用する形態です。利用者はインフラやアプリケーション実装を意識せず、機能を使います。

| 種類 | 利用者が主に管理するもの | AWSで近い例 | 特徴 |
|---|---|---|---|
| IaaS | OS、ミドルウェア、アプリ | EC2 | 自由度が高い |
| PaaS | アプリ、設定 | Lambda、Elastic Beanstalk | 管理負担が少ない |
| SaaS | 利用設定、データ | Amazon Qなど | すぐ使いやすい |

## 1.4 従量課金と初期投資

![1.4 従量課金と初期投資](/images/aws-study/fig_045_aws_learning.png)


AWSの多くのサービスは従量課金です。従量課金とは、利用した時間、容量、リクエスト数、データ転送量などに応じて料金が発生する仕組みです。

従量課金のメリットは、小さく始められることです。一方で、不要なリソースを放置すると料金が増えます。検証用に作成したEC2、NAT Gateway、RDS、EBSスナップショット、CloudWatch Logsなどは定期的に確認します。

**AWSでは、作る力と同じくらい、消す力が重要です。**

## 1.5 マネージドサービス

マネージドサービスとは、サーバーやソフトウェアの運用管理の一部をAWSが代わりに行うサービスです。Amazon RDSは、データベースエンジンのセットアップ、バックアップ、パッチ適用などを支援するマネージドデータベースです。

EC2上に自分でMySQLをインストールすることもできますが、その場合はOS、データベース、バックアップ、監視、障害対応を自分で設計します。RDSを使うと、これらの多くをAWSの機能として利用できます。

**実務では、特別な理由がなければマネージドサービスを優先するのが基本です。**

## 1.6 AWSの主要カテゴリ

AWSサービスは、コンピューティング、ストレージ、データベース、ネットワーク、セキュリティ、運用管理、開発者ツール、分析、AI/MLに分けると理解しやすくなります。

- コンピューティング：EC2、Lambda、ECS、EKSなど、処理を実行するサービスです。
- ストレージ：S3、EBS、EFSなど、データを保存するサービスです。
- データベース：RDS、Aurora、DynamoDBなど、構造化されたデータを扱います。
- ネットワーク：VPC、Route 53、CloudFront、ELBなど、通信を制御します。
- セキュリティ：IAM、KMS、WAF、GuardDutyなど、権限や防御を担います。
- 運用管理：CloudWatch、CloudTrail、Config、Systems Managerなど、監視と管理を担います。

---

# 第2章 AWSの基本用語とサービス地図

![第2章 AWSの基本用語とサービス地図](/images/aws-study/fig_004_aws.png)


## 2.1 サービスとリソース

![2.1 サービスとリソース](/images/aws-study/fig_046_aws_learning.png)


AWSのサービスとは、EC2、S3、RDS、Lambdaのような機能のまとまりです。リソースとは、そのサービスを使って作成した具体的な実体です。

たとえば、EC2はサービス名で、起動した仮想サーバー1台はEC2インスタンスというリソースです。S3はサービス名で、作成したバケットや保存したオブジェクトがリソースです。

**AWSでは、サービス名とリソース名を区別して理解することが重要です。**料金、権限、監視、削除の対象になるのは、多くの場合リソースです。

## 2.2 リージョン、アベイラビリティゾーン、エッジロケーション

![2.2 リージョン、アベイラビリティゾーン、エッジロケーション](/images/aws-study/fig_047_aws_learning.png)


リージョンとは、AWSのデータセンター群が存在する地理的な地域です。東京リージョン、大阪リージョン、バージニア北部リージョンなどがあります。

アベイラビリティゾーンは、リージョン内にある独立したデータセンター群です。AZと略されます。1つのAZで障害が起きても、別のAZでシステムを動かせるように設計できます。

エッジロケーションとは、ユーザーに近い場所でコンテンツ配信や名前解決などを行う拠点です。CloudFrontやRoute 53などで使われます。

**リージョンは場所、AZは障害に備える単位、エッジロケーションはユーザーに近づける単位**と覚えると整理しやすいです。

## 2.3 グローバルサービスとリージョンサービス

![2.3 グローバルサービスとリージョンサービス](/images/aws-study/fig_048_aws_learning.png)


AWSサービスには、グローバルサービスとリージョンサービスがあります。グローバルサービスは、特定リージョンだけに閉じないサービスです。IAMやRoute 53は代表例です。

リージョンサービスは、リソースを作成するリージョンを選ぶサービスです。EC2、RDS、VPC、Lambdaなどは基本的にリージョンを意識します。リソースが見つからないときは、まずリージョンを確認します。

## 2.4 ARN、アカウントID、リソースID

![2.4 ARN、アカウントID、リソースID](/images/aws-study/fig_049_aws_learning.png)


ARNはAmazon Resource Nameの略で、AWSリソースを一意に表す名前です。IAMポリシーやログで頻繁に登場します。

```text
arn:aws:s3:::example-bucket
arn:aws:lambda:ap-northeast-1:123456789012:function:my-function
```

ARNは、AWS内での住所のようなものです。どのサービスの、どのリージョンの、どのアカウントの、どのリソースかを表します。

## 2.5 タグによる管理

タグは、AWSリソースに付けるキーと値のラベルです。たとえば、`Environment=Production`、`Owner=AppTeam`、`Project=SalesSystem`のように設定します。

タグは、検索、権限管理、コスト配分、運用自動化に使えます。実務では、タグがないと誰のリソースなのか、削除してよいのか、どのシステムの費用なのかが分からなくなります。

## 2.6 AWSを操作する方法

AWSの操作方法は、AWSマネジメントコンソール、AWS CLI、AWS SDK、IaCの4つです。初心者はコンソールで理解し、次にCLIで確認し、実務ではIaCで再現可能にする流れが効率的です。

```bash
aws sts get-caller-identity
aws ec2 describe-regions --all-regions
```

`sts get-caller-identity`は、現在どのAWS認証情報で操作しているかを確認する基本コマンドです。

## 2.7 可用性、耐久性、レイテンシー、スループット

可用性とは、システムが使える状態を維持できる度合いです。耐久性とは、保存したデータが失われにくい度合いです。レイテンシーとは、リクエストしてから応答が返るまでの遅延です。スループットとは、一定時間に処理できる量です。

Webサイトにたとえると、画面が開くまでの待ち時間がレイテンシーで、同時にどれだけ多くの利用者を処理できるかがスループットです。

## 2.8 認証、認可、監査、暗号化

認証とは、誰であるかを確認することです。認可とは、認証された利用者に何を許可するかを決めることです。監査とは、誰が、いつ、何をしたかを記録し、後から確認できるようにすることです。暗号化とは、データを第三者が読めない形式に変換することです。

**セキュリティは、認証、認可、監査、暗号化の4つで考えると整理しやすいです。**

---

# 第3章 AWSアカウント作成と安全な初期設定

![第3章 AWSアカウント作成と安全な初期設定](/images/aws-study/fig_005_aws.png)


## 3.1 ルートユーザーとIAMユーザー

![3.1 ルートユーザーとIAMユーザー](/images/aws-study/fig_050_iam.png)


ルートユーザーは、AWSアカウント作成時に作られる最上位のユーザーです。請求情報、アカウント解約、重要なセキュリティ設定など、非常に強い権限を持ちます。

IAMユーザーは、AWS Identity and Access Managementで作成する利用者です。通常の作業では、ルートユーザーを使わず、IAMユーザーやIAM Identity Centerを使います。

**ルートユーザーは日常作業に使いません。金庫の鍵のように保管し、必要なときだけ使います。**

## 3.2 MFAの必須化

![3.2 MFAの必須化](/images/aws-study/fig_051_aws_learning.png)


MFAはMulti-Factor Authenticationの略で、多要素認証のことです。パスワードに加えて、認証アプリやセキュリティキーなど別の要素で本人確認します。

AWSアカウントでは、ルートユーザーに必ずMFAを設定します。管理者権限を持つユーザーにもMFAを設定します。パスワードだけの認証は、漏えいした瞬間に突破される可能性があるためです。

## 3.3 IAM Identity Center

![3.3 IAM Identity Center](/images/aws-study/fig_052_iam.png)


IAM Identity Centerは、複数のAWSアカウントやアプリケーションへのアクセスを一元管理するサービスです。以前はAWS Single Sign-Onと呼ばれていました。

実務では、個別にIAMユーザーを大量作成するよりも、IAM Identity Centerで利用者と権限セットを管理する方が安全です。退職者や異動者のアクセス削除もしやすくなります。

## 3.4 予算アラートと請求アラート

![3.4 予算アラートと請求アラート](/images/aws-study/fig_053_aws_learning.png)


AWSでは、リソースを作ると料金が発生します。学習環境でもNAT Gateway、RDS、EC2、EBS、CloudWatch Logsなどで料金が発生することがあります。

AWS Budgetsを使うと、月額予算を超えそうなときに通知できます。初心者は、最初に必ず予算アラートを設定します。

**AWS学習の最初のハンズオンは、EC2作成ではなく予算アラート作成です。**

## 3.5 無料利用枠の注意点

AWSには無料利用枠があります。ただし、すべてが無料になるわけではありません。無料枠の対象サービス、対象サイズ、対象期間、上限を超えた利用は課金されます。

また、無料利用枠の範囲でも、関連サービスで料金が発生する場合があります。EC2を停止しても、EBSボリュームが残っていると課金対象になる場合があります。

## 3.6 CloudTrailの初期有効化

CloudTrailは、AWSアカウント内で実行されたAPI操作を記録するサービスです。誰が、いつ、どのサービスに、どのような操作をしたかを追跡できます。

不正操作や誤操作の調査では、CloudTrailが非常に重要です。学習環境でも、本番環境でも、監査ログを残す習慣を持ちます。

## 3.7 AWS CLIとCloudShell

AWS CLIは、コマンドラインからAWSを操作するツールです。CloudShellは、ブラウザから利用できるAWS管理用のシェル環境です。

```bash
aws configure
aws sts get-caller-identity
```

アクセスキーをローカルPCに保存する場合は、取り扱いに注意します。実務では、IAM Identity Centerや一時認証情報、OIDCを使い、長期アクセスキーを減らす設計が望ましいです。

## 3.8 不要リソースの削除

AWSでは、リソース削除の確認が重要です。EC2を終了してもEBSスナップショットが残る、ALBを消してもターゲットグループが残る、CloudWatch Logsが残るなど、関連リソースが残ることがあります。

学習後は、EC2、EBS、Elastic IP、NAT Gateway、RDS、S3、Load Balancer、CloudWatch Logsを確認します。

---

# 第4章 グローバルインフラとリージョン設計

![第4章 グローバルインフラとリージョン設計](/images/aws-study/fig_006_chapter.png)


## 4.1 リージョン選択の基準

![4.1 リージョン選択の基準](/images/aws-study/fig_054_aws_learning.png)


リージョンは、システムを配置する地理的な単位です。リージョン選択では、利用者との距離、法規制、利用したいサービスの提供状況、コスト、障害対策を考えます。

日本の利用者向けサービスでは東京リージョンを選ぶことが多いです。西日本に災害対策拠点を置きたい場合、大阪リージョンも候補になります。

**リージョンは近ければよいだけではありません。可用性、法務、コスト、サービス提供状況を含めて選びます。**

## 4.2 アベイラビリティゾーンとマルチAZ

![4.2 アベイラビリティゾーンとマルチAZ](/images/aws-study/fig_055_aws_learning.png)


アベイラビリティゾーンは、リージョン内の独立した設備群です。AZ間は低遅延のネットワークで接続されています。

マルチAZとは、複数のAZにリソースを分散する構成です。1つのAZで障害が発生しても、別のAZでサービスを継続しやすくなります。

たとえば、Webサーバーを2つのAZに配置し、ALBで振り分ける構成にすると、片方のAZで障害が起きても、もう片方で応答できます。

## 4.3 Local Zones、Wavelength、Outposts

![4.3 Local Zones、Wavelength、Outposts](/images/aws-study/fig_056_aws_learning.png)


Local Zonesは、特定都市の近くで低遅延アプリケーションを動かすための拠点です。Wavelengthは、5Gネットワークに近い場所でアプリケーションを動かし、超低遅延を狙う仕組みです。

Outpostsは、AWSのインフラやサービスをオンプレミス環境に拡張するサービスです。法規制や低遅延要件でオンプレミスに機器を置きたい場合に使います。

## 4.4 RTOとRPO

![4.4 RTOとRPO](/images/aws-study/fig_057_aws_learning.png)


RTOはRecovery Time Objectiveの略で、障害発生後にどれくらいの時間で復旧する必要があるかを表します。

RPOはRecovery Point Objectiveの略で、どれくらい前のデータまで失ってよいかを表します。

**RTOは時間の停止許容、RPOはデータ損失の許容です。**この2つはDR設計の出発点です。

## 4.5 DRの基本

DRはDisaster Recoveryの略で、災害復旧のことです。大規模障害、リージョン障害、人的ミス、ランサムウェアなどに備える設計です。

| DR方式 | 復旧速度 | コスト | 概要 |
|---|---|---|---|
| バックアップ＆リストア | 遅い | 低い | バックアップから復元する |
| パイロットライト | 中程度 | 中程度 | 最小構成を常時用意する |
| ウォームスタンバイ | 速い | 高い | 縮小版の本番環境を待機させる |
| アクティブ/アクティブ | 非常に速い | 非常に高い | 複数環境で同時稼働する |

**復元できることを定期的に確認する復元テストが必要です。**

---

# 第5章 責任共有モデルとセキュリティ基礎

![第5章 責任共有モデルとセキュリティ基礎](/images/aws-study/fig_007_security.png)


## 5.1 責任共有モデル

![5.1 責任共有モデル](/images/aws-study/fig_058_aws_learning.png)


責任共有モデルとは、AWSと利用者がそれぞれどの範囲を守るかを分ける考え方です。AWSはクラウド基盤そのものを守り、利用者はクラウド上に作る設定やデータを守ります。

AWSは、データセンター、物理サーバー、ネットワーク設備、仮想化基盤などを管理します。一方、利用者はIAM権限、S3公開設定、OSパッチ、アプリケーション、データ暗号化、ログ確認などを担当します。

**AWSを使うだけで安全になるのではなく、安全に設定して初めて安全になります。**

## 5.2 サービスによって責任範囲は変わる

![5.2 サービスによって責任範囲は変わる](/images/aws-study/fig_059_aws_learning.png)


EC2では、利用者がOSの更新、ミドルウェア設定、セキュリティパッチ、ウイルス対策などを管理します。

RDSでは、データベースエンジンの管理やバックアップ機能の多くをAWSが支援します。ただし、パラメータ設定、アクセス制御、データ内容、接続元制限は利用者の責任です。

Lambdaでは、サーバー管理の負担はさらに小さくなります。ただし、実行ロール、コードの脆弱性、環境変数、入力検証は利用者が管理します。

## 5.3 最小権限

![5.3 最小権限](/images/aws-study/fig_060_aws_learning.png)


最小権限とは、利用者やサービスに必要最低限の権限だけを付与する考え方です。ログを読むだけの担当者に、EC2削除権限やIAM変更権限を与えるべきではありません。

最小権限は、事故の影響範囲を小さくします。権限が強すぎると、誤操作や不正利用による被害が大きくなります。

## 5.4 多層防御

![5.4 多層防御](/images/aws-study/fig_061_aws_learning.png)


多層防御とは、1つの防御策に依存せず、複数の防御を重ねる考え方です。WAF、ALB、セキュリティグループ、IAM、KMS、CloudTrail、CloudWatchを組み合わせます。

**どれか1つが破られても、次の防御で止める設計が大切です。**

## 5.5 暗号化と監査ログ

![5.5 暗号化と監査ログ](/images/aws-study/fig_062_encryption.png)


暗号化には、保存時の暗号化と通信時の暗号化があります。保存時の暗号化は、S3やEBS、RDSに保存されたデータを暗号化することです。通信時の暗号化は、HTTPSやTLSで通信内容を保護することです。

監査ログは、操作履歴を後から確認するための記録です。AWSではCloudTrailが中心になります。ログがないと、原因調査も再発防止も困難になります。

---

# 第6章 IAMを絶対に理解する

![第6章 IAMを絶対に理解する](/images/aws-study/fig_008_iam.png)


## 6.1 IAMとは何か

![6.1 IAMとは何か](/images/aws-study/fig_063_iam.png)


IAMはIdentity and Access Managementの略で、AWSにおける認証と認可を管理するサービスです。誰がAWSへアクセスできるか、その人やサービスが何をできるかを決めます。

IAMはAWS学習の最重要項目です。IAMを理解しないままAWSを使うと、権限エラーで作業が止まるだけでなく、過剰権限による事故につながります。

## 6.2 認証と認可

![6.2 認証と認可](/images/aws-study/fig_064_auth.png)


認証は、アクセスしている相手が誰かを確認することです。認可は、認証された相手に何を許可するかを決めることです。

たとえるなら、認証は会社の入口で社員証を確認すること、認可はその社員がどの部屋に入れるかを決めることです。

## 6.3 IAMユーザー、グループ、ロール

![6.3 IAMユーザー、グループ、ロール](/images/aws-study/fig_065_iam.png)


IAMユーザーは、人やアプリケーションに対応する個別のIDです。IAMグループは、複数のIAMユーザーに同じ権限を付けるためのまとまりです。IAMロールは、一時的に引き受ける権限です。

**人にはユーザーまたはIdentity Center、AWSサービスにはロール、という考え方が基本です。**

## 6.4 IAMポリシー

![6.4 IAMポリシー](/images/aws-study/fig_066_iam.png)


IAMポリシーは、どの操作をどのリソースに対して許可または拒否するかをJSONで書いたものです。

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": "arn:aws:s3:::example-bucket/*"
    }
  ]
}
```

`Effect`は許可か拒否を表します。`Action`は操作内容です。`Resource`は対象リソースです。`Condition`を使うと、条件付きで許可できます。

## 6.5 デフォルトDeny、明示的Allow、明示的Deny

![6.5 デフォルトDeny、明示的Allow、明示的Deny](/images/aws-study/fig_067_aws_learning.png)


AWSの権限評価では、基本的に何も許可されていなければ拒否されます。これをデフォルトDenyまたは暗黙的Denyと呼びます。

操作を許可するには、ポリシーで明示的にAllowする必要があります。ただし、どこかに明示的Denyがある場合、AllowよりもDenyが優先されます。

- 何も書いていない：拒否
- Allowがある：許可候補
- Denyがある：必ず拒否

**IAMの権限評価では、明示的Denyが最強です。**

## 6.6 アイデンティティベースポリシーとリソースベースポリシー

![6.6 アイデンティティベースポリシーとリソースベースポリシー](/images/aws-study/fig_068_aws_learning.png)


アイデンティティベースポリシーは、IAMユーザー、グループ、ロールに付けるポリシーです。リソースベースポリシーは、S3バケットやSQSキュー、KMSキーなど、リソース側に付けるポリシーです。

プリンシパルとは、AWSへリクエストを行う主体です。IAMユーザー、IAMロール、AWSサービス、別アカウントなどが該当します。

## 6.7 信頼ポリシー

![6.7 信頼ポリシー](/images/aws-study/fig_069_aws_learning.png)


信頼ポリシーは、IAMロールを誰が引き受けられるかを定義するポリシーです。ロールには、権限ポリシーと信頼ポリシーがあります。

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "lambda.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

`sts:AssumeRole`は、ロールを引き受けるための操作です。

## 6.8 パーミッションバウンダリーとSCP

パーミッションバウンダリーは、IAMユーザーやロールに設定する権限の上限です。SCPはService Control Policyの略で、AWS Organizationsで使うアカウント全体の権限上限です。

たとえるなら、IAMポリシーは社員への作業許可、パーミッションバウンダリーはその社員の職務上限、SCPは会社全体の禁止ルールです。

## 6.9 EC2ロールとLambda実行ロール

EC2からS3へアクセスするとき、アクセスキーをEC2内に保存するのは危険です。代わりにEC2にIAMロールを付与します。Lambda実行ロールは、Lambda関数がAWSサービスへアクセスするためのロールです。

**AWSサービスからAWSサービスへアクセスするときは、長期アクセスキーではなくIAMロールを使います。**

## 6.10 クロスアカウントロールとAccess Analyzer

クロスアカウントロールは、別のAWSアカウントからロールを引き受ける仕組みです。監査アカウントから本番アカウントを参照する、CI/CDアカウントから開発アカウントへデプロイするなどの用途で使います。

IAM Access Analyzerは、外部からアクセス可能なリソースや過剰な権限を検出するためのサービスです。IAMは一度設定して終わりではなく、定期的に権限を見直します。

---

# 第7章 VPCとネットワーク基礎

![第7章 VPCとネットワーク基礎](/images/aws-study/fig_009_vpc.png)


## 7.1 VPCとは何か

![7.1 VPCとは何か](/images/aws-study/fig_070_vpc.png)


VPCはVirtual Private Cloudの略で、AWS上に作る論理的に隔離された仮想ネットワークです。EC2、RDS、ECSなど多くのリソースはVPC内に配置します。

**VPCはAWSネットワークの土台です。VPCを理解すると、EC2、RDS、ALB、ECSの構成が一気に理解しやすくなります。**

## 7.2 CIDR、IPv4、IPv6

![7.2 CIDR、IPv4、IPv6](/images/aws-study/fig_071_aws_learning.png)


CIDRはClassless Inter-Domain Routingの略で、IPアドレス範囲を表す記法です。たとえば`10.0.0.0/16`は、10.0.0.0から始まる大きなIP範囲を表します。

IPv4は、`192.168.1.10`のような形式のIPアドレスです。IPv6は、より広いアドレス空間を持つ新しい形式です。

## 7.3 パブリックIPとプライベートIP

![7.3 パブリックIPとプライベートIP](/images/aws-study/fig_072_aws_learning.png)


パブリックIPは、インターネットから到達可能なIPアドレスです。プライベートIPは、VPC内など閉じたネットワークで使うIPアドレスです。

DBサーバーにパブリックIPを付けるのは危険です。通常、RDSなどのデータベースはプライベートサブネットに配置し、アプリケーションからのみ接続させます。

## 7.4 サブネット

![7.4 サブネット](/images/aws-study/fig_073_aws_learning.png)


サブネットは、VPCのIPアドレス範囲を分割したものです。サブネットは1つのAZに属します。

パブリックサブネットは、インターネットへ直接出入りできる経路を持つサブネットです。プライベートサブネットは、インターネットから直接到達できないサブネットです。

## 7.5 ルートテーブルとInternet Gateway

![7.5 ルートテーブルとInternet Gateway](/images/aws-study/fig_074_aws_learning.png)


ルートテーブルは、通信をどこへ送るかを決める表です。Internet Gatewayは、VPCとインターネットを接続するためのゲートウェイです。

パブリックサブネットにするには、ルートテーブルに`0.0.0.0/0 -> Internet Gateway`のような経路を設定します。`0.0.0.0/0`は、すべてのIPv4宛先を意味します。

## 7.6 NAT Gateway

![7.6 NAT Gateway](/images/aws-study/fig_075_aws_learning.png)


NAT Gatewayは、プライベートサブネット内のリソースがインターネットへ出ていくためのサービスです。インターネットからプライベートサブネットへ直接入ってくる通信は許可しません。

NAT Gatewayは便利ですが、時間課金とデータ処理課金があります。検証環境で放置するとコストが増えやすいサービスです。

## 7.7 セキュリティグループとネットワークACL

![7.7 セキュリティグループとネットワークACL](/images/aws-study/fig_076_security.png)


セキュリティグループは、EC2やRDSなどのリソースに付ける仮想ファイアウォールです。許可ルールだけを書きます。状態を持つため、戻り通信は自動的に許可されます。

ネットワークACLは、サブネット単位で設定するファイアウォールです。許可と拒否の両方を書けます。状態を持たないため、戻り通信も明示的に考える必要があります。

| 項目 | セキュリティグループ | ネットワークACL |
|---|---|---|
| 適用単位 | リソース単位 | サブネット単位 |
| ルール | Allow中心 | AllowとDeny |
| 状態 | ステートフル | ステートレス |
| 主な用途 | 通信制御の中心 | 補助的な境界防御 |

## 7.8 VPCエンドポイントとPrivateLink

VPCエンドポイントは、インターネットを経由せずにVPCからAWSサービスへ接続する仕組みです。S3やDynamoDBにはゲートウェイエンドポイント、他の多くのサービスにはインターフェイスエンドポイントを使います。

PrivateLinkは、インターフェイスエンドポイントを使って、プライベートにサービスへ接続する仕組みです。

## 7.9 DNS、VPC Flow Logs、Reachability Analyzer

DNSはDomain Name Systemの略で、ドメイン名をIPアドレスに変換する仕組みです。Route 53 Resolverは、VPC内外の名前解決を扱うサービスです。

VPC Flow Logsは、VPC内のネットワークインターフェイスを通る通信のメタ情報を記録する機能です。Reachability Analyzerは、送信元から送信先までネットワーク的に到達可能かを分析するサービスです。

---

# 第8章 ネットワーク実務設計

![第8章 ネットワーク実務設計](/images/aws-study/fig_010_network.png)


## 8.1 3層ネットワーク

![8.1 3層ネットワーク](/images/aws-study/fig_077_network.png)


3層ネットワークは、Web層、アプリケーション層、データベース層に分ける設計です。Web層は外部からの入口、アプリケーション層は業務処理、データベース層はデータ保存を担当します。

AWSでは、ALBをパブリックサブネットに配置し、ECSやEC2をプライベートサブネットに配置し、RDSをさらに制限されたプライベートサブネットに配置する構成がよく使われます。

**外部公開するものを最小限にし、内部リソースはプライベートに置くことが基本です。**

## 8.2 マルチAZサブネット設計

![8.2 マルチAZサブネット設計](/images/aws-study/fig_078_aws_learning.png)


本番環境では、少なくとも2つのAZにサブネットを作成します。パブリックサブネット、アプリケーション用プライベートサブネット、DB用プライベートサブネットを各AZに用意すると、障害に強い構成になります。

- Public Subnet A、Public Subnet C
- App Private Subnet A、App Private Subnet C
- DB Private Subnet A、DB Private Subnet C

## 8.3 ALB配置

![8.3 ALB配置](/images/aws-study/fig_079_aws_learning.png)


ALBはApplication Load Balancerの略で、HTTP/HTTPS通信を複数のターゲットへ振り分けるロードバランサーです。ALBは通常、複数のパブリックサブネットに配置します。

ALBのセキュリティグループでは、インターネットからのHTTPSを許可し、アプリケーション側のセキュリティグループでは、ALBからの通信だけを許可します。

## 8.4 NAT Gateway配置

![8.4 NAT Gateway配置](/images/aws-study/fig_080_aws_learning.png)


NAT GatewayはAZごとに配置するのが可用性の観点では望ましいです。ただし、コストが増えます。

本番環境では各AZにNAT Gatewayを配置し、各プライベートサブネットから同じAZのNAT Gatewayへ出るようにします。開発環境ではコストを抑えるために1台だけにする場合もあります。

**可用性とコストは常にトレードオフです。環境ごとに判断します。**

## 8.5 VPCエンドポイントによるS3接続

![8.5 VPCエンドポイントによるS3接続](/images/aws-study/fig_081_vpc.png)


プライベートサブネットからS3へアクセスする場合、NAT Gateway経由にするとコストが増えることがあります。S3ゲートウェイエンドポイントを使うと、VPC内からS3へプライベートに接続できます。

## 8.6 踏み台サーバーとSession Manager

![8.6 踏み台サーバーとSession Manager](/images/aws-study/fig_082_aws_learning.png)


踏み台サーバーは、プライベートサブネット内のサーバーへ接続するための中継サーバーです。ただし、踏み台サーバー自体の管理やSSH鍵の管理が必要になります。

Session ManagerはSystems Managerの機能で、SSHポートを開けずにEC2へ接続できます。IAMで接続権限を制御でき、操作ログも残しやすくなります。

## 8.7 オンプレミス接続

![8.7 オンプレミス接続](/images/aws-study/fig_083_aws_learning.png)


オンプレミスとAWSを接続する方法には、Site-to-Site VPN、Client VPN、Direct Connectがあります。Transit Gatewayは、複数VPCやVPN、Direct Connectを集約するハブです。

## 8.8 ネットワーク障害の切り分け

通信できない場合は、送信元と送信先のIP、ポート、プロトコルを確認し、セキュリティグループ、NACL、ルートテーブル、DNS、アプリケーションの待ち受けを順番に確認します。

**ネットワーク障害は、感覚ではなく経路を1つずつ確認します。**

---

# 第9章 EC2と仮想サーバー

![第9章 EC2と仮想サーバー](/images/aws-study/fig_011_ec2.png)


## 9.1 EC2とは何か

![9.1 EC2とは何か](/images/aws-study/fig_084_ec2.png)


EC2はElastic Compute Cloudの略で、AWS上で仮想サーバーを起動するサービスです。OS、CPU、メモリ、ストレージ、ネットワークを選んでサーバーを作成できます。

EC2は自由度が高く、既存アプリケーションの移行や細かい設定が必要な用途に向いています。一方で、OSパッチやミドルウェア管理などの運用負担があります。

## 9.2 AMIとインスタンスタイプ

![9.2 AMIとインスタンスタイプ](/images/aws-study/fig_085_aws_learning.png)


AMIはAmazon Machine Imageの略で、EC2を起動するためのテンプレートです。OSや初期ソフトウェアが含まれます。

インスタンスタイプは、CPU、メモリ、ネットワーク性能などの組み合わせです。CPU重視ならC系、メモリ重視ならR系、汎用ならM系やT系など、用途に応じて選びます。

## 9.3 キーペア、SSH、RDP、Session Manager

![9.3 キーペア、SSH、RDP、Session Manager](/images/aws-study/fig_086_aws_learning.png)


キーペアは、EC2へSSH接続するための公開鍵と秘密鍵の組み合わせです。LinuxではSSH、WindowsではRDPを使うことが多いです。

鍵ファイルの漏えいは重大事故につながります。可能であればSession Managerを使い、SSHポートを開けない運用にします。

## 9.4 EBSとインスタンスストア

![9.4 EBSとインスタンスストア](/images/aws-study/fig_087_aws_learning.png)


EBSはElastic Block Storeの略で、EC2に接続するブロックストレージです。EC2を停止してもデータを保持できます。

インスタンスストアは、インスタンスに物理的に接続された一時ストレージです。高速ですが、停止や終了でデータが失われる場合があります。

## 9.5 ユーザーデータ

![9.5 ユーザーデータ](/images/aws-study/fig_088_data.png)


ユーザーデータは、EC2起動時に実行するスクリプトです。初回起動時にWebサーバーをインストールするなどの初期設定に使います。

```bash
#!/bin/bash
dnf update -y
dnf install -y nginx
systemctl enable nginx
systemctl start nginx
echo "Hello AWS" > /usr/share/nginx/html/index.html
```

ユーザーデータを使うと、手作業を減らし、同じ設定のサーバーを再現しやすくなります。

## 9.6 Auto Scaling Group

![9.6 Auto Scaling Group](/images/aws-study/fig_089_aws_learning.png)


Auto Scaling Groupは、EC2インスタンス数を自動で増減する仕組みです。負荷が高いときに増やし、低いときに減らせます。また、異常なインスタンスを置き換えることもできます。

## 9.7 Systems Managerとパッチ管理

![9.7 Systems Managerとパッチ管理](/images/aws-study/fig_090_aws_learning.png)


Systems Managerは、EC2やオンプレミスサーバーを管理するサービス群です。Session Manager、Run Command、Patch Managerなどがあります。

Patch Managerを使うと、OSパッチ適用を自動化できます。EC2を使う場合、OS管理は利用者の責任なので、パッチ運用を設計に含めます。

## 9.8 Spot、Savings Plans、Reserved Instances

Spot Instancesは、AWSの余剰キャパシティを安く使う仕組みです。ただし、中断される可能性があります。Savings PlansとReserved Instancesは、長期利用を前提に料金を下げる仕組みです。

## 9.9 EC2のアンチパターン

EC2に何でも入れる構成は、最初は簡単ですが、運用が重くなりやすいです。ログ、バックアップ、スケーリング、パッチ、障害復旧をすべて考える必要があります。

新規開発では、RDS、S3、Lambda、ECSなどのマネージドサービスを組み合わせ、EC2の管理範囲を減らすことを検討します。

---

# 第10章 ストレージ：S3、EBS、EFS、FSx、Backup

![第10章 ストレージ：S3、EBS、EFS、FSx、Backup](/images/aws-study/fig_012_s3.png)


## 10.1 ストレージの種類

![10.1 ストレージの種類](/images/aws-study/fig_091_aws_learning.png)


AWSのストレージは、オブジェクトストレージ、ブロックストレージ、ファイルストレージに分けると理解しやすいです。

| 種類 | 代表サービス | 主な用途 |
|---|---|---|
| オブジェクトストレージ | S3 | ファイル、ログ、画像、バックアップ、データレイク |
| ブロックストレージ | EBS | EC2のディスク |
| ファイルストレージ | EFS、FSx | 複数サーバーで共有するファイルシステム |

## 10.2 Amazon S3

![10.2 Amazon S3](/images/aws-study/fig_092_s3.png)


S3はSimple Storage Serviceの略で、オブジェクトストレージサービスです。大量のファイル、バックアップ、ログ、画像、動画、データレイクなどに使います。

```bash
aws s3 mb s3://example-learning-bucket
aws s3 cp ./sample.txt s3://example-learning-bucket/sample.txt
aws s3 ls s3://example-learning-bucket/
```

## 10.3 S3ストレージクラス

![10.3 S3ストレージクラス](/images/aws-study/fig_093_s3.png)


S3ストレージクラスは、アクセス頻度や復元時間に応じてコストを最適化するための保存クラスです。頻繁にアクセスするデータにはS3 Standard、アクセス頻度が低いデータにはStandard-IA、長期保管にはGlacier系のクラスを検討します。

ライフサイクルルールを使うと、一定期間後にストレージクラスを変更したり、古いオブジェクトを削除したりできます。

## 10.4 バージョニング、レプリケーション、暗号化

![10.4 バージョニング、レプリケーション、暗号化](/images/aws-study/fig_094_encryption.png)


バージョニングは、同じキーのオブジェクトを複数世代で保存する機能です。誤削除や誤更新から復旧しやすくなります。

レプリケーションは、別バケットや別リージョンへオブジェクトを複製する機能です。DRやコンプライアンス目的で使います。

S3では保存時暗号化を有効化できます。SSE-S3、SSE-KMSなどの方式があります。

## 10.5 パブリックアクセスブロックとバケットポリシー

![10.5 パブリックアクセスブロックとバケットポリシー](/images/aws-study/fig_095_aws_learning.png)


S3の公開設定ミスは重大な情報漏えいにつながります。パブリックアクセスブロックは、意図しない公開を防ぐ重要な機能です。

バケットポリシーは、バケットに対するアクセス制御をJSONで定義するリソースベースポリシーです。

**S3は便利ですが、公開設定を誤ると危険です。原則は非公開です。**

## 10.6 署名付きURLと静的Webサイトホスティング

![10.6 署名付きURLと静的Webサイトホスティング](/images/aws-study/fig_096_aws_learning.png)


署名付きURLは、一定時間だけS3オブジェクトへアクセスできるURLです。非公開ファイルを一時的に配布するときに使います。

静的Webサイトホスティングは、S3バケットを使ってHTML、CSS、JavaScriptなどの静的サイトを公開する機能です。HTTPSや独自ドメインを使う場合はCloudFrontやACMと組み合わせるのが一般的です。

## 10.7 EBS、EFS、FSx、AWS Backup

![10.7 EBS、EFS、FSx、AWS Backup](/images/aws-study/fig_097_aws.png)


EBSはEC2に接続するブロックストレージです。EBSスナップショットは、EBSボリュームのバックアップです。

EFSはLinux向けの共有ファイルストレージです。FSxは、用途別の高機能ファイルストレージです。

AWS Backupは、複数のAWSサービスのバックアップを一元管理するサービスです。**復元できることまで確認して初めてバックアップです。**

---

# 第11章 データベース：RDS、Aurora、DynamoDB

![第11章 データベース：RDS、Aurora、DynamoDB](/images/aws-study/fig_013_rds.png)


## 11.1 RDBとNoSQL

![11.1 RDBとNoSQL](/images/aws-study/fig_098_aws_learning.png)


RDBはRelational Databaseの略で、テーブル、行、列、SQLを使ってデータを扱うデータベースです。NoSQLは、RDBとは異なる柔軟なデータモデルを持つデータベースの総称です。

| 観点 | RDB | NoSQL |
|---|---|---|
| 代表サービス | RDS、Aurora | DynamoDB |
| 得意な処理 | 複雑な検索、結合、トランザクション | 高スケールな読み書き、単純なアクセス |
| 設計の起点 | 正規化、SQL | アクセスパターン、キー設計 |
| 注意点 | スケール設計 | キー設計の失敗 |

## 11.2 Amazon RDS

![11.2 Amazon RDS](/images/aws-study/fig_099_rds.png)


RDSはRelational Database Serviceの略で、マネージドなリレーショナルデータベースです。MySQL、PostgreSQL、MariaDB、Oracle、SQL Serverなどを利用できます。

RDSでは、DBインスタンス、DBサブネットグループ、パラメータグループ、オプショングループ、セキュリティグループを理解します。通常、RDSは複数AZのプライベートサブネットに配置します。

## 11.3 バックアップ、スナップショット、マルチAZ

![11.3 バックアップ、スナップショット、マルチAZ](/images/aws-study/fig_100_aws_learning.png)


RDSの自動バックアップは、指定した保持期間内でポイントインタイムリカバリを可能にします。ポイントインタイムリカバリとは、特定時刻の状態へ戻すことです。

マルチAZは、スタンバイDBを別AZに用意し、障害時にフェイルオーバーする構成です。フェイルオーバーとは、障害時に待機系へ切り替えることです。

## 11.4 リードレプリカ

![11.4 リードレプリカ](/images/aws-study/fig_101_aws_learning.png)


リードレプリカは、読み取り負荷を分散するための複製DBです。検索やレポート処理など、読み取りが多いシステムで使います。

**マルチAZは可用性向上、リードレプリカは主に読み取り性能向上のための機能です。**

## 11.5 Amazon Aurora

![11.5 Amazon Aurora](/images/aws-study/fig_102_aws_learning.png)


Auroraは、AWSがクラウド向けに設計したリレーショナルデータベースです。MySQL互換とPostgreSQL互換があります。

Auroraは、ストレージが分散され、高い可用性と性能を目指した設計です。Aurora Serverlessを使うと、需要に応じて容量を自動調整しやすくなります。

## 11.6 DynamoDB

![11.6 DynamoDB](/images/aws-study/fig_103_dynamodb.png)


DynamoDBは、フルマネージドなNoSQLデータベースです。高いスケーラビリティと低レイテンシーを必要とする用途に向いています。

DynamoDBでは、テーブル、項目、属性、パーティションキー、ソートキーを理解します。パーティションキーはデータの分散と検索の基本になるキーです。ソートキーは、同じパーティションキー内でデータを並べたり範囲検索したりするためのキーです。

## 11.7 GSIとLSI

![11.7 GSIとLSI](/images/aws-study/fig_104_aws_learning.png)


GSIはGlobal Secondary Indexの略で、別のキーで検索できるようにするインデックスです。LSIはLocal Secondary Indexの略で、同じパーティションキーを使いながら別のソートキーで検索するインデックスです。

**DynamoDBでは、後から自由にSQL検索するのではなく、最初にアクセスパターンを決めてキー設計します。**

## 11.8 オンデマンドとプロビジョンド

オンデマンドモードは、リクエスト量に応じて自動的に処理能力が調整される課金方式です。予測しにくい負荷に向いています。

プロビジョンドモードは、読み書きキャパシティをあらかじめ設定する方式です。負荷が予測できる場合にコストを抑えやすいです。

## 11.9 周辺データベースサービス

ElastiCacheは、RedisやMemcached互換のキャッシュサービスです。DocumentDBはMongoDB互換のドキュメントデータベースです。Neptuneはグラフデータベースです。Redshiftはデータウェアハウスです。Timestreamは時系列データベースです。OpenSearch Serviceは検索とログ分析に使います。

---

# 第12章 ELB、Route 53、CloudFront、ACMで公開する

![第12章 ELB、Route 53、CloudFront、ACMで公開する](/images/aws-study/fig_014_route53.png)


## 12.1 DNSとRoute 53

![12.1 DNSとRoute 53](/images/aws-study/fig_105_route53.png)


DNSは、ドメイン名をIPアドレスなどに変換する仕組みです。Route 53は、AWSのDNSサービスです。

ホストゾーンは、ドメインのDNSレコードを管理する入れ物です。Aレコードは名前をIPv4アドレスへ対応させ、CNAMEは別名を設定します。Aliasレコードは、ALBやCloudFrontなどAWSリソースへ名前を向けるときに便利です。

## 12.2 ルーティングポリシー

![12.2 ルーティングポリシー](/images/aws-study/fig_106_aws_learning.png)


Route 53のルーティングポリシーを使うと、単純な名前解決だけでなく、加重ルーティング、レイテンシーベースルーティング、フェイルオーバールーティングなどができます。

## 12.3 ACMとTLS証明書

![12.3 ACMとTLS証明書](/images/aws-study/fig_107_aws_learning.png)


ACMはAWS Certificate Managerの略で、TLS証明書を管理するサービスです。TLS証明書は、HTTPS通信でサーバーの正当性を証明し、通信を暗号化するために使います。

## 12.4 ELB、ALB、NLB

![12.4 ELB、ALB、NLB](/images/aws-study/fig_108_aws_learning.png)


ELBはElastic Load Balancingの総称です。通信を複数のターゲットへ分散します。

| 種類 | 主な用途 | 特徴 |
|---|---|---|
| ALB | HTTP/HTTPS | パスやホスト名で振り分けできる |
| NLB | TCP/UDP | 高性能で固定IPが必要な用途にも使える |
| CLB | 旧世代 | 新規では基本的にALB/NLBを検討する |

ターゲットグループは、ALBやNLBが通信を振り分ける先のまとまりです。ヘルスチェックにより、異常なターゲットへ通信を流さないようにできます。

## 12.5 CloudFrontとCDN

CloudFrontは、AWSのCDNサービスです。CDNはContent Delivery Networkの略で、ユーザーに近いエッジロケーションからコンテンツを配信し、表示速度や可用性を高める仕組みです。

CloudFrontの配信元をオリジンと呼びます。S3、ALB、EC2、カスタムサーバーなどをオリジンにできます。キャッシュを使うと、同じコンテンツへのアクセスを高速化し、オリジンへの負荷を減らせます。

## 12.6 OACと署名付きURL

OACはOrigin Access Controlの略で、CloudFrontからS3オリジンへ安全にアクセスするための仕組みです。S3を直接公開せず、CloudFront経由だけで配信できます。

署名付きURLは、一定条件や一定時間だけアクセスできるURLです。有料コンテンツや限定配布に使えます。

## 12.7 WAFとShield

WAFはWeb Application Firewallの略で、SQLインジェクションやクロスサイトスクリプティングなどのWeb攻撃を検出・遮断するサービスです。

ShieldはDDoS攻撃から保護するサービスです。DDoSはDistributed Denial of Serviceの略で、大量の通信でサービスを妨害する攻撃です。

---

# 第13章 可用性、スケーリング、耐障害性

![第13章 可用性、スケーリング、耐障害性](/images/aws-study/fig_015_chapter.png)


## 13.1 可用性と単一障害点

![13.1 可用性と単一障害点](/images/aws-study/fig_109_aws_learning.png)


可用性は、システムが利用可能な状態を維持する度合いです。単一障害点は、そこが壊れるとシステム全体が止まる箇所です。

EC2が1台だけ、DBが1台だけ、特定AZだけに配置、手動復旧が必要、といった構成は単一障害点になりやすいです。

**止めたくないシステムでは、単一障害点を見つけて減らすことが基本です。**

## 13.2 スケールアップとスケールアウト

![13.2 スケールアップとスケールアウト](/images/aws-study/fig_110_aws_learning.png)


スケールアップは、サーバーをより高性能なものに変更する方法です。スケールアウトは、サーバー台数を増やす方法です。

クラウドでは、スケールアウトしやすい設計が重要です。そのためには、アプリケーションをステートレスに近づけます。

## 13.3 ステートレス設計とセッション管理

![13.3 ステートレス設計とセッション管理](/images/aws-study/fig_111_aws_learning.png)


ステートレスとは、サーバーが利用者ごとの状態を持たない設計です。どのサーバーにリクエストが届いても同じように処理できます。

セッション情報を各EC2のメモリに持つと、別のEC2へ振り分けられたときにログイン状態が失われることがあります。セッションはElastiCacheやDynamoDBなど外部ストアに持たせるとスケールしやすくなります。

## 13.4 キューによる疎結合

![13.4 キューによる疎結合](/images/aws-study/fig_112_aws_learning.png)


キューは、処理待ちのメッセージを一時的にためる仕組みです。SQSを使うと、急激なアクセス増加や処理遅延を吸収できます。

注文受付処理でメール送信や在庫更新を同期的にすべて行うと、どこかが遅いだけで注文受付が遅くなります。SQSにメッセージを入れ、後続処理を非同期化すると、受付処理を安定させやすくなります。

## 13.5 バックアップ戦略とDR戦略

バックアップは、データを復旧するための基本です。RDSスナップショット、S3バージョニング、EBSスナップショット、AWS Backupなどを使います。

DR戦略では、復旧時間とコストのバランスを考えます。重要なシステムほど、複数AZや複数リージョンを使った構成を検討します。

## 13.6 障害テスト

設計上は冗長化していても、実際に切り替わるとは限りません。Auto Scaling、RDSフェイルオーバー、復元手順、アラーム通知などはテストします。

**障害は起きない前提ではなく、障害が起きても被害を小さくする前提で設計します。**

---

# 第14章 サーバーレス：Lambda、API Gateway、EventBridge

![第14章 サーバーレス：Lambda、API Gateway、EventBridge](/images/aws-study/fig_016_lambda.png)


## 14.1 サーバーレスとは何か

![14.1 サーバーレスとは何か](/images/aws-study/fig_113_serverless.png)


サーバーレスとは、サーバーが存在しないという意味ではなく、サーバーの管理を利用者が直接行わない設計です。AWSが実行基盤を管理し、利用者はコードや設定に集中します。

Lambda、API Gateway、DynamoDB、S3、SQS、EventBridgeなどを組み合わせると、サーバー管理を大幅に減らしたアプリケーションを作れます。

## 14.2 Lambda

![14.2 Lambda](/images/aws-study/fig_114_lambda.png)


Lambdaは、イベントに応じてコードを実行するサーバーレスコンピューティングサービスです。HTTPリクエスト、S3イベント、DynamoDB Streams、SQSメッセージなどをきっかけに実行できます。

```python
def lambda_handler(event, context):
    name = event.get("name", "AWS")
    return {
        "statusCode": 200,
        "body": f"Hello {name}"
    }
```

## 14.3 実行ロール、環境変数、タイムアウト

![14.3 実行ロール、環境変数、タイムアウト](/images/aws-study/fig_115_aws_learning.png)


Lambda実行ロールは、LambdaがAWSサービスへアクセスするためのIAMロールです。DynamoDBへ書き込むならDynamoDBへの権限、CloudWatch Logsへログを書き込むならログ権限が必要です。

環境変数は、コード外から設定値を渡す仕組みです。タイムアウトは、Lambdaが最大何秒実行できるかの設定です。

## 14.4 同時実行数とコールドスタート

![14.4 同時実行数とコールドスタート](/images/aws-study/fig_116_aws_learning.png)


同時実行数は、Lambdaが同時に処理できる実行数です。アクセスが急増すると、同時実行数も増えます。

コールドスタートは、新しい実行環境を初期化するために発生する遅延です。重い初期化処理がある関数では影響する場合があります。

## 14.5 API Gateway

![14.5 API Gateway](/images/aws-study/fig_117_aws_learning.png)


API Gatewayは、HTTP APIを作成・公開するサービスです。Lambdaと組み合わせると、サーバーレスAPIを構築できます。

HTTP APIはシンプルで低コストな用途に向き、REST APIはより豊富な機能が必要な用途に向きます。

## 14.6 EventBridge

![14.6 EventBridge](/images/aws-study/fig_118_aws_learning.png)


EventBridgeは、イベント駆動アーキテクチャを作るためのイベントバスサービスです。イベントバスとは、イベントを受け取り、ルールに応じて宛先へ配信する仕組みです。

## 14.7 SQS、SNS、Step Functions

![14.7 SQS、SNS、Step Functions](/images/aws-study/fig_119_aws_learning.png)


SQSはメッセージキューです。SNSはPub/Sub型の通知サービスです。Step Functionsは、複数の処理を状態遷移として定義するサービスです。

## 14.8 冪等性、リトライ、DLQ

冪等性とは、同じ処理を複数回実行しても結果が変わらない性質です。DLQはDead Letter Queueの略で、処理に失敗したメッセージを退避するキューです。

**イベント駆動では、失敗と再実行を前提に設計します。**

---

# 第15章 コンテナ：ECS、Fargate、EKS、ECR

![第15章 コンテナ：ECS、Fargate、EKS、ECR](/images/aws-study/fig_017_ecs.png)


## 15.1 コンテナとは何か

![15.1 コンテナとは何か](/images/aws-study/fig_120_container.png)


コンテナは、アプリケーションと実行に必要なライブラリや設定をひとまとめにして動かす仕組みです。環境差分を減らし、開発環境と本番環境で同じように動かしやすくなります。

Dockerイメージは、コンテナを起動するためのテンプレートです。

## 15.2 Dockerfile

![15.2 Dockerfile](/images/aws-study/fig_121_aws_learning.png)


Dockerfileは、Dockerイメージを作るための手順書です。

```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
CMD ["python", "app.py"]
```

## 15.3 ECR

![15.3 ECR](/images/aws-study/fig_122_aws_learning.png)


ECRはElastic Container Registryの略で、Dockerイメージを保存するレジストリです。ECSやEKSからECRに保存したイメージを取得してコンテナを起動します。

ECRにはイメージスキャン機能があり、コンテナイメージに含まれる脆弱性を検出できます。

## 15.4 ECS

![15.4 ECS](/images/aws-study/fig_123_ecs.png)


ECSはElastic Container Serviceの略で、AWSのコンテナオーケストレーションサービスです。コンテナの起動、停止、配置、スケーリングを管理します。

ECSの主要用語は、クラスター、タスク定義、タスク、サービスです。タスク定義はコンテナの設計書、タスクは実行中のコンテナ、サービスはタスクを指定数維持する仕組みです。

## 15.5 Fargate

![15.5 Fargate](/images/aws-study/fig_124_aws_learning.png)


Fargateは、サーバー管理なしでECSやEKSのコンテナを実行する起動方式です。EC2インスタンスを自分で管理せず、タスク単位でCPUやメモリを指定します。

## 15.6 タスクロールとタスク実行ロール

![15.6 タスクロールとタスク実行ロール](/images/aws-study/fig_125_aws_learning.png)


タスクロールは、コンテナ内のアプリケーションがAWSサービスへアクセスするためのIAMロールです。タスク実行ロールは、ECSがECRからイメージを取得したり、CloudWatch Logsへログを送ったりするためのロールです。

**アプリ用がタスクロール、ECS基盤用がタスク実行ロール**です。

## 15.7 EKSとApp Runner

![15.7 EKSとApp Runner](/images/aws-study/fig_126_eks.png)


EKSはElastic Kubernetes Serviceの略で、AWS上でKubernetesを運用するマネージドサービスです。Kubernetesは、コンテナを大規模に管理するオープンソースの仕組みです。

App Runnerは、コンテナやソースコードからWebアプリを簡単に公開できるサービスです。

## 15.8 デプロイ戦略

コンテナでは、ローリングデプロイ、Blue/Greenデプロイ、Canaryデプロイなどを使います。

| 方式 | 概要 | 特徴 |
|---|---|---|
| Rolling | 少しずつ置き換える | 標準的で扱いやすい |
| Blue/Green | 新旧環境を切り替える | 戻しやすい |
| Canary | 一部通信から段階拡大 | リスクを抑えやすい |

---

---

[後編へ進む](/articles/aws-study-guide-02)
