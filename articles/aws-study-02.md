---
title: "絶対にわかるAWS 学習資料 後編"
emoji: "☁️"
type: "tech"
topics: ["aws", "初心者", "クラウド", "インフラ"]
published: false
---

[前編へ戻る](/articles/aws-study)

## このシリーズについて

この記事は「絶対にわかるAWS 学習資料」の後編です。第16章〜最終まとめまでを扱います。

- [前編: はじめに〜第15章](/articles/aws-study)
- [後編: 第16章〜最終まとめ](/articles/aws-study-02)

# 第16章 アプリケーション統合とイベント設計

![第16章 アプリケーション統合とイベント設計](/images/aws-study/fig_018_chapter.png)


## 16.1 疎結合

![16.1 疎結合](/images/aws-study/fig_127_aws_learning.png)


疎結合とは、システムの部品同士の依存を弱くする設計です。あるサービスが一時的に遅くなっても、全体に影響しにくくなります。

密結合な設計では、注文受付、在庫更新、メール送信、請求処理がすべて同期的につながり、どこかが失敗すると全体が失敗します。疎結合では、キューやイベントで処理を分離します。

## 16.2 SQS

![16.2 SQS](/images/aws-study/fig_128_aws_learning.png)


SQSはSimple Queue Serviceの略です。メッセージをキューにため、処理側が順番に取り出します。

標準キューは高スループットで、メッセージ順序や重複排除は厳密ではありません。FIFOキューは順序保証と重複排除を重視します。

## 16.3 DLQ

![16.3 DLQ](/images/aws-study/fig_129_aws_learning.png)


DLQは、何度処理しても失敗するメッセージを退避するキューです。失敗メッセージを本流から分離し、後から原因を調査できます。

## 16.4 SNS

![16.4 SNS](/images/aws-study/fig_130_aws_learning.png)


SNSはSimple Notification Serviceの略で、Pub/Sub型のメッセージ配信サービスです。Pub/Subとは、発行者がメッセージを出し、購読者が受け取る仕組みです。

SNSからSQS、Lambda、メール、HTTPエンドポイントなどへ配信できます。

## 16.5 EventBridge

EventBridgeは、イベントをルールで振り分けるサービスです。AWSサービスのイベント、独自アプリのイベント、SaaSのイベントを扱えます。

## 16.6 Step Functions

Step Functionsは、ワークフローを状態として定義するサービスです。状態遷移、分岐、並列処理、待機、リトライ、エラー処理を明示できます。

## 16.7 オーケストレーションとコレオグラフィ

オーケストレーションは、中央の司令塔が処理順序を管理する方式です。Step Functionsが代表例です。

コレオグラフィは、各サービスがイベントに反応して自律的に動く方式です。EventBridgeやSNSを使う構成が近いです。

---

# 第17章 開発者ツールとCI/CD

![第17章 開発者ツールとCI/CD](/images/aws-study/fig_019_chapter.png)


## 17.1 CI/CD

![17.1 CI/CD](/images/aws-study/fig_131_aws_learning.png)


CIはContinuous Integrationの略で、継続的インテグレーションです。コード変更を頻繁に統合し、自動テストやビルドを行います。

CDはContinuous DeliveryまたはContinuous Deploymentの略です。ビルド済みアプリケーションを安全にデプロイする仕組みです。

**CI/CDの目的は、手作業を減らし、変更を小さく速く安全に届けることです。**

## 17.2 Gitとブランチ戦略

![17.2 Gitとブランチ戦略](/images/aws-study/fig_132_aws_learning.png)


Gitはソースコードの変更履歴を管理するツールです。ブランチは、作業の流れを分けるための枝です。

小さなチームでは、mainブランチとfeatureブランチを使い、Pull Requestでレビューしてからマージする方式が分かりやすいです。

## 17.3 CodePipeline、CodeBuild、CodeDeploy

![17.3 CodePipeline、CodeBuild、CodeDeploy](/images/aws-study/fig_133_aws_learning.png)


CodePipelineは、ソース取得、ビルド、テスト、デプロイなどの流れをつなぐサービスです。CodeBuildは、ビルドやテストを実行するサービスです。CodeDeployは、EC2、ECS、Lambdaなどへのデプロイを支援します。

```yaml
version: 0.2
phases:
  install:
    runtime-versions:
      python: 3.12
  build:
    commands:
      - pip install -r requirements.txt
      - pytest
artifacts:
  files:
    - '**/*'
```

## 17.4 デプロイ方式

![17.4 デプロイ方式](/images/aws-study/fig_134_aws_learning.png)


Rollingデプロイは、少しずつ新バージョンへ置き換える方式です。Blue/Greenデプロイは、新旧環境を用意し、通信を切り替える方式です。Canaryデプロイは、一部の利用者だけ新バージョンへ流し、問題がなければ徐々に拡大します。

## 17.5 GitHub ActionsとOIDC

![17.5 GitHub ActionsとOIDC](/images/aws-study/fig_135_aws_learning.png)


GitHub ActionsからAWSへデプロイする場合、長期アクセスキーをGitHub Secretsに保存する方式は漏えいリスクがあります。

OIDCを使うと、GitHub Actionsが一時的にAWSロールを引き受けられます。**CI/CDでは、長期アクセスキーを減らし、一時認証情報を使うことが重要です。**

## 17.6 Secrets ManagerとParameter Store

![17.6 Secrets ManagerとParameter Store](/images/aws-study/fig_136_aws_learning.png)


Secrets Managerは、DBパスワードやAPIキーなどの機密情報を管理するサービスです。Parameter Storeは、設定値や一部の機密値を管理できるSystems Managerの機能です。

機密情報をソースコードやコンテナイメージに埋め込んではいけません。

---

# 第18章 監視、ログ、監査：CloudWatch、CloudTrail、Config

![第18章 監視、ログ、監査：CloudWatch、CloudTrail、Config](/images/aws-study/fig_020_cloudwatch.png)


## 18.1 メトリクス、ログ、トレース

![18.1 メトリクス、ログ、トレース](/images/aws-study/fig_137_aws_learning.png)


メトリクスは、CPU使用率、リクエスト数、エラー数のような数値データです。ログは、アプリケーションやシステムが出力する記録です。トレースは、1つのリクエストが複数サービスをまたいでどう処理されたかを追跡する情報です。

監視では、メトリクスで異常を検知し、ログで原因を調べ、トレースで処理の流れを追います。

## 18.2 CloudWatch MetricsとAlarms

![18.2 CloudWatch MetricsとAlarms](/images/aws-study/fig_138_cloudwatch.png)


CloudWatch Metricsは、AWSリソースやアプリケーションの数値データを収集します。CloudWatch Alarmsは、メトリクスがしきい値を超えたときに通知や自動処理を行います。

## 18.3 CloudWatch LogsとLogs Insights

![18.3 CloudWatch LogsとLogs Insights](/images/aws-study/fig_139_cloudwatch.png)


CloudWatch Logsは、ログを収集・保存するサービスです。Logs Insightsは、CloudWatch Logsに対してクエリを実行する機能です。

```sql
fields @timestamp, @message
| filter @message like /ERROR/
| sort @timestamp desc
| limit 20
```

## 18.4 CloudTrail

![18.4 CloudTrail](/images/aws-study/fig_140_cloudtrail.png)


CloudTrailは、AWS API操作を記録する監査サービスです。コンソール操作、CLI操作、SDK操作の多くはAPIとして記録されます。

誤ってS3バケットが公開された、IAMポリシーが変更された、RDSが削除された、という場合に、誰がいつ操作したかを確認できます。

## 18.5 AWS Config

![18.5 AWS Config](/images/aws-study/fig_141_aws.png)


AWS Configは、AWSリソースの設定履歴を記録し、ルールに基づいて準拠状況を評価するサービスです。

たとえば、S3バケットが公開されていないか、EBSが暗号化されているか、セキュリティグループでSSHが全開放されていないかを継続的に確認できます。

## 18.6 X-RayとSystems Manager

![18.6 X-RayとSystems Manager](/images/aws-study/fig_142_aws_learning.png)


X-Rayは、分散アプリケーションのトレースを収集するサービスです。Systems Managerは、運用管理のためのサービス群です。Session Manager、Run Command、Patch Managerなどがあります。

## 18.7 監視設計

![18.7 監視設計](/images/aws-study/fig_143_monitoring.png)


監視設計では、何を検知したいのかを先に決めます。重要なのは、可用性、レイテンシー、エラー率、飽和度です。

---

# 第19章 セキュリティサービス実践

![第19章 セキュリティサービス実践](/images/aws-study/fig_021_security.png)


## 19.1 KMS

![19.1 KMS](/images/aws-study/fig_144_aws_learning.png)


KMSはKey Management Serviceの略で、暗号鍵を管理するサービスです。S3、EBS、RDS、Lambda環境変数など、多くのサービスでKMSキーを利用できます。

KMSでは、キーポリシーとIAMポリシーの両方を理解する必要があります。

## 19.2 Secrets Manager

![19.2 Secrets Manager](/images/aws-study/fig_145_aws_learning.png)


Secrets Managerは、DBパスワードやAPIキーなどの機密情報を安全に保存するサービスです。アプリケーションはSecrets Managerから実行時に値を取得します。

```python
import boto3

client = boto3.client("secretsmanager")
response = client.get_secret_value(SecretId="prod/db/password")
secret = response["SecretString"]
```

## 19.3 WAF、Shield、Network Firewall

![19.3 WAF、Shield、Network Firewall](/images/aws-study/fig_146_aws_learning.png)


WAFはWebアプリケーションへの攻撃を防ぐサービスです。ShieldはDDoS保護サービスです。Network Firewallは、VPCレベルでより高度なネットワーク制御を行うマネージドファイアウォールです。

## 19.4 GuardDuty

![19.4 GuardDuty](/images/aws-study/fig_147_aws_learning.png)


GuardDutyは、脅威検出サービスです。CloudTrail、VPC Flow Logs、DNSログなどを分析し、不審な操作や通信を検出します。

## 19.5 Security Hub

![19.5 Security Hub](/images/aws-study/fig_148_aws_learning.png)


Security Hubは、複数のセキュリティサービスの検出結果を集約し、セキュリティ基準に照らして評価するサービスです。

## 19.6 Inspector、Macie、Detective

![19.6 Inspector、Macie、Detective](/images/aws-study/fig_149_aws_learning.png)


Inspectorは、EC2、ECR、Lambdaなどの脆弱性を検出するサービスです。Macieは、S3内の機密データを検出するサービスです。Detectiveは、セキュリティインシデントの調査を支援するサービスです。

## 19.7 インシデント対応

![19.7 インシデント対応](/images/aws-study/fig_150_aws_learning.png)


インシデント対応では、検知、封じ込め、調査、復旧、再発防止を行います。CloudTrail、GuardDuty、Security Hub、VPC Flow Logs、CloudWatch Logsを使って証跡を確認します。

**平常時からログを残し、調査できる状態を作ります。**

---

# 第20章 コスト管理とクラウド財務管理

![第20章 コスト管理とクラウド財務管理](/images/aws-study/fig_022_cost.png)


## 20.1 従量課金を理解する

![20.1 従量課金を理解する](/images/aws-study/fig_151_aws_learning.png)


AWSでは、リソースの稼働時間、保存容量、リクエスト数、データ転送量などに応じて料金が発生します。

コスト管理の基本は、何に料金が発生しているかを把握することです。請求画面だけでなく、Cost Explorer、Budgets、タグを使って確認します。

## 20.2 Cost Explorer

![20.2 Cost Explorer](/images/aws-study/fig_152_aws_learning.png)


Cost Explorerは、AWS利用料金を可視化するサービスです。サービス別、アカウント別、タグ別、期間別にコストを確認できます。

コストが急増した場合、まずCost Explorerでどのサービスが増えたかを確認します。

## 20.3 AWS BudgetsとCost Anomaly Detection

![20.3 AWS BudgetsとCost Anomaly Detection](/images/aws-study/fig_153_aws.png)


AWS Budgetsは、予算を設定し、超過しそうなときに通知するサービスです。Cost Anomaly Detectionは、通常と異なるコスト増加を検出するサービスです。

## 20.4 タグによるコスト配分

![20.4 タグによるコスト配分](/images/aws-study/fig_154_cost.png)


タグを使うと、プロジェクト別、環境別、チーム別にコストを集計できます。

- `Project=PaymentSystem`
- `Environment=Production`
- `Owner=BackendTeam`

## 20.5 コストが増えやすいポイント

![20.5 コストが増えやすいポイント](/images/aws-study/fig_155_cost.png)


初心者が見落としやすいコストには、NAT Gateway、未使用EBS、古いスナップショット、RDSの起動しっぱなし、ALBの放置、CloudWatch Logsの長期保管、データ転送料があります。

**AWSコストは、作ったものではなく、残っているものから発生し続けます。**

## 20.6 Savings Plans、Reserved Instances、Spot

![20.6 Savings Plans、Reserved Instances、Spot](/images/aws-study/fig_156_aws_learning.png)


Savings Plansは、一定のコンピューティング利用を約束して割引を受ける仕組みです。Reserved Instancesは、特定条件のリソースを長期利用する前提で割引を受ける仕組みです。Spotは、余剰キャパシティを安く使う仕組みです。

## 20.7 FinOps

![20.7 FinOps](/images/aws-study/fig_157_aws_learning.png)


FinOpsは、クラウドの技術利用とコスト管理を結びつける考え方です。単に安くするのではなく、必要な性能や可用性を満たしながら無駄を減らすことが重要です。

---

# 第21章 IaC：CloudFormation、CDK、SAM、Terraform

![第21章 IaC：CloudFormation、CDK、SAM、Terraform](/images/aws-study/fig_023_iac.png)


## 21.1 IaCとは何か

![21.1 IaCとは何か](/images/aws-study/fig_158_iac.png)


IaCはInfrastructure as Codeの略で、インフラ構成をコードとして管理する考え方です。手作業で画面から作るのではなく、テンプレートやプログラムでAWSリソースを定義します。

**本番環境では、手作業で作ったリソースより、コードで再現できるリソースの方が管理しやすいです。**

## 21.2 CloudFormation

![21.2 CloudFormation](/images/aws-study/fig_159_aws_learning.png)


CloudFormationは、AWS公式のIaCサービスです。テンプレートにリソースを定義し、スタックとして作成します。

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Resources:
  SampleBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !Sub 'sample-bucket-${AWS::AccountId}-${AWS::Region}'
```

Resourcesは作成するリソースを定義するセクションです。Parametersは外部から渡す値、Outputsは作成後に出力する値です。

## 21.3 RefとFn::GetAtt

![21.3 RefとFn::GetAtt](/images/aws-study/fig_160_aws_learning.png)


`Ref`は、リソースやパラメータを参照する関数です。`Fn::GetAtt`は、リソースの属性を取得する関数です。

## 21.4 Change SetsとDrift Detection

![21.4 Change SetsとDrift Detection](/images/aws-study/fig_161_aws_learning.png)


Change Setsは、スタック更新前に何が変更されるかを確認する機能です。Drift Detectionは、CloudFormationで管理している状態と実際のリソース状態がずれていないかを確認する機能です。

## 21.5 CDK

![21.5 CDK](/images/aws-study/fig_162_aws_learning.png)


CDKはCloud Development Kitの略で、TypeScript、Python、Javaなどのプログラミング言語でAWSリソースを定義するツールです。

Constructは、CDKで使う部品です。Stackは、デプロイ単位です。Appは、複数のStackを含むCDKアプリ全体です。

## 21.6 SAM

![21.6 SAM](/images/aws-study/fig_163_aws_learning.png)


SAMはServerless Application Modelの略で、サーバーレスアプリケーション向けのIaCフレームワークです。Lambda、API Gateway、DynamoDBなどを簡潔に定義できます。

## 21.7 Terraform

![21.7 Terraform](/images/aws-study/fig_164_aws_learning.png)


Terraformは、HashiCorpが提供するIaCツールです。AWSだけでなく複数クラウドやSaaSを管理できます。

| ツール | 主な用途 | 特徴 |
|---|---|---|
| CloudFormation | AWS公式IaC | AWSとの統合が強い |
| CDK | プログラムでAWS定義 | 抽象化しやすい |
| SAM | サーバーレス | Lambda中心に扱いやすい |
| Terraform | 複数基盤管理 | State管理が重要 |

---

# 第22章 Organizations、Control Tower、マルチアカウント

![第22章 Organizations、Control Tower、マルチアカウント](/images/aws-study/fig_024_chapter.png)


## 22.1 マルチアカウントの必要性

![22.1 マルチアカウントの必要性](/images/aws-study/fig_165_aws_learning.png)


AWSでは、1つのアカウントにすべてを詰め込むより、用途ごとにアカウントを分ける設計が推奨されます。

開発、本番、監査、ログ、ネットワーク、セキュリティなどを分けると、権限、請求、障害影響、監査を分離しやすくなります。

**アカウントは単なる契約単位ではなく、強力な分離境界です。**

## 22.2 AWS Organizations

![22.2 AWS Organizations](/images/aws-study/fig_166_aws.png)


AWS Organizationsは、複数のAWSアカウントを一元管理するサービスです。管理アカウントとメンバーアカウントで構成されます。

OUはOrganizational Unitの略で、アカウントをまとめる単位です。一括請求により、複数アカウントの請求をまとめられます。

## 22.3 SCP

![22.3 SCP](/images/aws-study/fig_167_aws_learning.png)


SCPはService Control Policyの略で、アカウントやOUに適用する権限の上限です。

SCPは権限を付与するものではありません。**SCPは最大権限を制限するもの**です。

## 22.4 Control Tower

![22.4 Control Tower](/images/aws-study/fig_168_aws_learning.png)


Control Towerは、AWSのマルチアカウント環境を標準的な構成で作成・管理するサービスです。

ランディングゾーンは、安全なマルチアカウント環境の土台です。Account Factoryは、新しいアカウントを標準化して作成する機能です。

## 22.5 ログアーカイブ、監査、ネットワークアカウント

![22.5 ログアーカイブ、監査、ネットワークアカウント](/images/aws-study/fig_169_network.png)


ログアーカイブアカウントは、CloudTrailやConfigなどのログを集約するアカウントです。監査アカウントは、セキュリティチームや監査担当が各アカウントを確認するためのアカウントです。

ネットワークアカウントは、Transit Gateway、共有VPC、Direct Connectなど、共通ネットワークを管理するために使うことがあります。

---

# 第23章 ガバナンスと社内運用ルール

![第23章 ガバナンスと社内運用ルール](/images/aws-study/fig_025_chapter.png)


## 23.1 ガバナンスとは何か

![23.1 ガバナンスとは何か](/images/aws-study/fig_170_aws_learning.png)


ガバナンスとは、組織としてAWSを安全かつ効率的に使うためのルール、仕組み、監視のことです。

自由に使える環境は便利ですが、ルールがないと、権限過剰、公開ミス、コスト増加、命名不統一、ログ不足が起きます。

## 23.2 命名規則とタグ標準

![23.2 命名規則とタグ標準](/images/aws-study/fig_171_aws_learning.png)


命名規則は、リソース名を一貫した形式にするルールです。

```text
{system}-{env}-{component}-{region}
payment-prod-api-apne1
```

タグ標準では、Project、Environment、Owner、CostCenter、ManagedByなどを定義します。

## 23.3 暗号化、ログ、バックアップ標準

![23.3 暗号化、ログ、バックアップ標準](/images/aws-study/fig_172_encryption.png)


暗号化標準では、S3、EBS、RDS、DynamoDBなどで保存時暗号化を有効にする方針を定めます。

ログ保存期間は、セキュリティ要件や法令に応じて決めます。バックアップ標準では、対象、頻度、保持期間、復元テストの頻度を決めます。

## 23.4 変更管理

![23.4 変更管理](/images/aws-study/fig_173_aws_learning.png)


変更管理は、本番環境への変更を安全に行うための手続きです。変更内容、影響範囲、リリース手順、切り戻し手順、承認者を明確にします。

## 23.5 職務分掌と権限レビュー

職務分掌は、1人に強すぎる権限を集中させない考え方です。権限レビューでは、定期的にIAMユーザー、ロール、アクセスキー、管理者権限を棚卸しします。

## 23.6 自動修復

Config RulesやEventBridge、Lambdaを使うと、望ましくない設定を検出して自動修復できます。たとえば、S3バケットが公開されたら自動でパブリックアクセスブロックを有効化する、といった運用ができます。

---

# 第24章 分析基盤：S3、Glue、Athena、Redshift、QuickSight

![第24章 分析基盤：S3、Glue、Athena、Redshift、QuickSight](/images/aws-study/fig_026_s3.png)


## 24.1 データレイクとDWH

![24.1 データレイクとDWH](/images/aws-study/fig_174_data.png)


データレイクは、構造化データ、半構造化データ、非構造化データをそのまま蓄積する場所です。AWSではS3をデータレイクの中心にすることが多いです。

DWHはData Warehouseの略で、分析に適した形に整理されたデータ基盤です。Redshiftが代表です。

## 24.2 ETLとELT

![24.2 ETLとELT](/images/aws-study/fig_175_aws_learning.png)


ETLはExtract、Transform、Loadの略で、データを抽出し、変換し、格納する処理です。ELTは、先にデータを格納し、その後で変換する方式です。

## 24.3 ファイル形式とパーティション

![24.3 ファイル形式とパーティション](/images/aws-study/fig_176_aws_learning.png)


分析基盤では、CSVだけでなくParquetのような列指向フォーマットを使うと、クエリ性能とコストを改善しやすくなります。

パーティションは、日付やカテゴリなどでデータを分割する仕組みです。Athenaで日付パーティションを使うと、必要な範囲だけ読み取り、コストを抑えられます。

## 24.4 Glue

![24.4 Glue](/images/aws-study/fig_177_aws_learning.png)


Glueは、データ統合とETLのためのサービスです。Glue Data Catalogは、テーブル定義やスキーマ情報を管理するメタデータカタログです。

Glue Crawlerは、S3上のデータをスキャンしてスキーマを推測し、Data Catalogに登録します。Glue Jobは、データ変換処理を実行します。

## 24.5 Athena

![24.5 Athena](/images/aws-study/fig_178_aws_learning.png)


Athenaは、S3上のデータに対してSQLを実行できるサービスです。サーバーを管理せず、クエリ単位で利用できます。

```sql
SELECT status, count(*)
FROM access_logs
WHERE dt = '2026-05-13'
GROUP BY status;
```

Athenaは読み取ったデータ量に応じて料金が発生するため、Parquet化やパーティション設計が重要です。

## 24.6 RedshiftとQuickSight

![24.6 RedshiftとQuickSight](/images/aws-study/fig_179_aws_learning.png)


Redshiftは、分析用のデータウェアハウスです。QuickSightは、BIダッシュボードを作成するサービスです。AthenaやRedshiftなどのデータを可視化できます。

## 24.7 Kinesis、Firehose、MSK

![24.7 Kinesis、Firehose、MSK](/images/aws-study/fig_180_aws_learning.png)


Kinesis Data Streamsは、リアルタイムストリーミングデータを処理するサービスです。Data Firehoseは、ストリーミングデータをS3、Redshift、OpenSearchなどへ配信するサービスです。

MSKはManaged Streaming for Apache Kafkaの略で、Kafkaをマネージドで利用するサービスです。

---

# 第25章 AI/MLと生成AI：Bedrock、SageMaker AI、Amazon Q

![第25章 AI/MLと生成AI：Bedrock、SageMaker AI、Amazon Q](/images/aws-study/fig_027_chapter.png)


## 25.1 AI、ML、生成AI

AIはArtificial Intelligenceの略で、人工知能を意味します。MLはMachine Learningの略で、データからパターンを学習する機械学習です。

生成AIは、文章、画像、コード、音声などを生成するAIです。基盤モデルはFoundation Modelとも呼ばれ、大量データで事前学習された大規模モデルです。

## 25.2 推論、ファインチューニング、RAG

推論とは、学習済みモデルに入力を与えて出力を得ることです。ファインチューニングは、既存モデルを追加データで調整することです。

RAGはRetrieval-Augmented Generationの略で、検索で取得した外部情報を使って生成AIに回答させる方式です。社内文書やFAQを参照するAIでよく使います。

## 25.3 Amazon Bedrock

Amazon Bedrockは、複数の基盤モデルをAPI経由で利用し、生成AIアプリケーションを構築するためのマネージドサービスです。

モデル選択、ナレッジベース、エージェント、ガードレールなどの機能があります。

## 25.4 SageMaker AI

SageMaker AIは、機械学習モデルの構築、学習、デプロイ、運用を支援するサービスです。

トレーニングジョブはモデル学習を実行する処理です。エンドポイントは、学習済みモデルを推論APIとして公開する仕組みです。MLOpsは、機械学習の開発、デプロイ、監視、再学習を継続的に行う運用方法です。

## 25.5 Amazon Q

Amazon Qは、業務支援や開発支援に使える生成AIアシスタント群です。利用時は、アクセス権限、データ接続、機密情報、回答の正確性を必ず確認します。

## 25.6 AIセキュリティとAIコスト

生成AIでは、プロンプトインジェクション、機密情報漏えい、不正確な回答、過剰なAPI利用コストに注意します。

**AI機能は便利ですが、必ず人間の確認、アクセス制御、ログ、コスト上限、入力検証を設計します。**

---

# 第26章 専門カテゴリの全体像

![第26章 専門カテゴリの全体像](/images/aws-study/fig_028_chapter.png)


## 26.1 IoT

IoTはInternet of Thingsの略で、センサーや機器をインターネットに接続してデータを収集・制御する分野です。

IoT Coreは、デバイスとAWSを安全に接続するサービスです。IoT Greengrassは、エッジデバイス上でローカル処理を行うために使います。IoT Device Defenderは、デバイスのセキュリティ監視に使います。

## 26.2 メディアサービス

MediaConvertは、動画ファイルの変換に使います。MediaLiveは、ライブ動画処理に使います。IVSはInteractive Video Serviceの略で、低遅延のライブ配信を構築できます。

## 26.3 エンドユーザーコンピューティング

WorkSpacesは、クラウド上の仮想デスクトップサービスです。AppStream 2.0は、アプリケーションをストリーミング配信するサービスです。WorkSpaces Secure Browserは、安全なブラウザアクセス環境を提供するサービスです。

## 26.4 モバイル・Webアプリ支援

Amplifyは、Webアプリやモバイルアプリのフロントエンド開発、ホスティング、認証、API連携を支援するサービスです。Cognitoは、アプリケーションのユーザー認証やユーザー管理を行うサービスです。AppSyncは、GraphQL APIを提供するサービスです。

## 26.5 その他の専門サービス

Amazon Connectは、クラウドコンタクトセンターサービスです。GameLift Serversは、ゲームサーバー運用を支援します。Amazon Braketは量子コンピューティング関連サービスです。AWS Ground Stationは衛星通信データの受信に使います。

---

# 第27章 移行とハイブリッドクラウド

![第27章 移行とハイブリッドクラウド](/images/aws-study/fig_029_migration.png)


## 27.1 移行の7R

移行の7Rは、既存システムをクラウドへ移す方法を分類する考え方です。代表的には、Rehost、Replatform、Refactor、Repurchase、Retire、Retain、Relocateがあります。

Rehostは、既存サーバーを大きく変えずEC2などへ移す方法です。Replatformは、少し構成を変更してマネージドサービスを利用する方法です。Refactorは、アプリケーションを作り直してクラウドに最適化する方法です。

## 27.2 移行計画

移行では、対象システム、依存関係、データ量、停止可能時間、切り戻し手順を確認します。依存関係を調査しないまま移行すると、移行後に外部システム接続やバッチ処理が動かないことがあります。

## 27.3 Application Migration Service

Application Migration Serviceは、既存サーバーをAWSへ移行するためのサービスです。サーバー単位の移行に向いています。

## 27.4 Database Migration Service

DMSはDatabase Migration Serviceの略で、データベース移行を支援するサービスです。CDCを使うと、移行元DBの変更を継続的に移行先へ反映できます。

CDCはChange Data Captureの略で、変更データを捕捉する仕組みです。Schema Conversion Toolは、異なるDBエンジン間のスキーマ変換を支援します。

## 27.5 DataSync、Transfer Family、Snow Family

DataSyncは、オンプレミスや他ストレージからAWSへデータを転送するサービスです。Transfer Familyは、SFTP、FTPS、FTPでS3やEFSへファイル転送するサービスです。

Snow Familyは、大容量データを物理デバイスでAWSへ移すためのサービス群です。

## 27.6 ハイブリッド接続

ハイブリッドクラウドでは、オンプレミスとAWSを組み合わせます。VPN、Direct Connect、Transit Gateway、Route 53 Resolver、Storage Gatewayなどを使います。

---

# 第28章 Well-Architected Frameworkで設計評価

![第28章 Well-Architected Frameworkで設計評価](/images/aws-study/fig_030_well_architected.png)


## 28.1 Well-Architected Frameworkとは

Well-Architected Frameworkは、AWS上のシステムを良い設計に近づけるためのベストプラクティス集です。6つの柱に基づいて設計を評価します。

6つの柱は、運用上の優秀性、セキュリティ、信頼性、パフォーマンス効率、コスト最適化、持続可能性です。

**Well-Architectedは、完成後の採点ではなく、継続的に改善するための考え方です。**

## 28.2 運用上の優秀性

運用上の優秀性は、システムを効果的に運用し、継続的に改善する能力です。運用手順をコード化する、変更を小さくする、障害から学ぶ、メトリクスを使って改善する、といった実践が含まれます。

## 28.3 セキュリティ

セキュリティの柱では、ID管理、検知、防御、データ保護、インシデント対応を評価します。IAM最小権限、MFA、暗号化、CloudTrail、GuardDuty、WAF、Secrets Managerなどが関係します。

## 28.4 信頼性

信頼性は、障害から復旧し、需要の変化に対応し、期待通りに機能する能力です。マルチAZ、Auto Scaling、バックアップ、DR、SQSによる疎結合、障害テストが重要です。

## 28.5 パフォーマンス効率

パフォーマンス効率は、リソースを効率的に使って要件を満たす能力です。適切なインスタンスタイプ、キャッシュ、CDN、データベース設計、サーバーレス、マネージドサービス選択が関係します。

## 28.6 コスト最適化

コスト最適化は、必要な価値を最小限の無駄で提供する能力です。Cost Explorer、Budgets、タグ、Savings Plans、不要リソース削除、S3ライフサイクル、ログ保持期間見直しが重要です。

## 28.7 持続可能性

持続可能性は、環境負荷を減らしながらシステムを運用する考え方です。不要なリソースを削除し、効率的なアーキテクチャを選び、過剰な計算や保管を避けます。

---

# 第29章 実践アーキテクチャ集

![第29章 実践アーキテクチャ集](/images/aws-study/fig_031_chapter.png)


## 29.1 静的Webサイト

静的Webサイトでは、S3にHTML、CSS、JavaScriptを保存し、CloudFrontで配信し、Route 53で独自ドメインを設定し、ACMでHTTPS化します。

S3は直接公開せず、CloudFront OACを使ってCloudFront経由だけでアクセスさせる構成が安全です。

## 29.2 3層Webアプリ

3層Webアプリでは、CloudFront、ALB、ECSまたはEC2、RDSを組み合わせます。

ALBはパブリックサブネットに配置し、アプリケーションはプライベートサブネットに配置し、RDSはDB用プライベートサブネットに配置します。

## 29.3 サーバーレスAPI

サーバーレスAPIでは、API Gateway、Lambda、DynamoDBを組み合わせます。小規模APIや急なアクセス変動があるサービスでは、サーバー管理を減らせるメリットがあります。

## 29.4 非同期バッチ

非同期バッチでは、S3、SQS、Lambda、Step Functionsを組み合わせます。S3にファイルがアップロードされたら処理を開始し、SQSで処理待ちを管理し、Lambdaで変換し、Step Functionsで全体の流れを管理します。

## 29.5 コンテナWebサービス

コンテナWebサービスでは、ECR、ECS Fargate、ALBを使います。CI/CDでDockerイメージをビルドし、ECRへプッシュし、ECSサービスを更新します。

## 29.6 データ分析基盤

データ分析基盤では、S3にデータを集め、Glueでカタログ化し、AthenaでSQL検索し、QuickSightで可視化します。大規模分析や高性能なDWHが必要な場合はRedshiftを使います。

## 29.7 生成AI社内FAQ

生成AI社内FAQでは、社内文書をS3に保存し、Bedrock Knowledge Basesなどで検索可能にし、LambdaやAPI Gateway、Cognitoと組み合わせて社内利用者向けに公開します。

**利用者が閲覧できない文書をAIが回答に使わないよう、データアクセス制御を設計します。**

---

# 第30章 トラブルシューティングと障害対応

![第30章 トラブルシューティングと障害対応](/images/aws-study/fig_032_troubleshooting.png)


## 30.1 基本手順

障害対応では、まず事象、影響範囲、発生時刻、直前の変更、再現条件を確認します。次に、仮説を立て、ログやメトリクスで確認します。

感覚で設定を変更すると、原因が分からなくなり、被害が広がることがあります。

## 30.2 EC2に接続できない

EC2へ接続できない場合は、インスタンス状態、パブリックIP、セキュリティグループ、NACL、ルートテーブル、OS側のSSHサービス、Session Manager設定を確認します。

## 30.3 ALB 5xx

ALBで502や503が出る場合、ターゲットが正常か、ヘルスチェックに成功しているか、アプリケーションが対象ポートで待ち受けているかを確認します。

## 30.4 RDSに接続できない

RDS接続不可では、DBエンドポイント、ポート、セキュリティグループ、サブネット、ルート、認証情報、DB状態を確認します。

## 30.5 Lambdaタイムアウト

Lambdaタイムアウトでは、外部API、DB接続、VPC設定、NAT Gateway、DNS、メモリ不足を確認します。

## 30.6 S3 AccessDenied

S3のAccessDeniedでは、IAMポリシー、バケットポリシー、ACL、KMSキー権限、Block Public Access、VPCエンドポイントポリシーを確認します。

## 30.7 IAM権限エラー

IAM権限エラーでは、エラーメッセージのActionとResourceを確認します。必要な権限がAllowされているか、明示的Denyがないか、SCPやパーミッションバウンダリーで制限されていないかを確認します。

## 30.8 コスト急増

コスト急増では、Cost Explorerでサービス別に確認します。NAT Gateway、データ転送、RDS、EC2、CloudWatch Logs、スナップショットがよくある原因です。

## 30.9 ポストモーテム

ポストモーテムは、障害後の振り返りです。原因、影響、検知方法、対応、再発防止策を整理します。目的は犯人探しではなく、仕組みを改善することです。

---

# 第31章 ハンズオン総合演習

![第31章 ハンズオン総合演習](/images/aws-study/fig_033_hands_on.png)


## 31.1 演習の進め方

ハンズオンでは、最初に予算アラートを作成し、作業後に必ずリソースを削除します。演習用環境は本番環境と分けます。

## 31.2 基礎セットアップ

```bash
aws sts get-caller-identity
aws configure list
aws ec2 describe-vpcs
```

現在の認証情報、CLI設定、既存VPCを確認します。

## 31.3 VPCとEC2 Webサーバー

VPC、パブリックサブネット、Internet Gateway、ルートテーブル、セキュリティグループを作成し、EC2を起動します。ユーザーデータでnginxをインストールし、ブラウザから表示確認します。

## 31.4 ALBとAuto Scaling

EC2を複数AZに配置し、ALBで振り分けます。Auto Scaling Groupで希望台数を維持します。1台を終了してもAuto Scalingで再作成されることを確認します。

## 31.5 RDS接続

RDSをプライベートサブネットに作成し、アプリケーション用セキュリティグループからの接続だけを許可します。

## 31.6 サーバーレスAPI

API Gateway、Lambda、DynamoDBを使って簡単なAPIを作ります。LambdaにはDynamoDBへの最小権限ロールを設定します。CloudWatch Logsで実行ログを確認します。

## 31.7 SQS非同期処理

APIで受け付けた処理をSQSへ送信し、別のLambdaで処理します。失敗時にはDLQへ送ります。

## 31.8 IaC化

手作業で作った構成をCloudFormationまたはCDKで再作成します。最初はS3バケットやLambdaなど小さなリソースから始め、最終的にVPC、ALB、ECS、RDSなどをコード化します。

## 31.9 監視と障害再現

CloudWatch Alarmを設定し、意図的にヘルスチェック失敗やLambdaエラーを発生させます。障害時にどのログを見るか、どのメトリクスを見るかを演習します。

## 31.10 リソース削除

演習後は、作成したリソースを削除します。CloudFormationやCDKで作ったものはスタック削除を使います。

---

# 第32章 AWSエンジニアの学習ロードマップ

![第32章 AWSエンジニアの学習ロードマップ](/images/aws-study/fig_034_aws.png)


## 32.1 入門段階

入門段階では、AWSの全体像、IAM、VPC、EC2、S3、RDS、CloudWatchを優先します。最初からすべてのサービスを深掘りする必要はありません。

## 32.2 基礎固め

基礎固めでは、IAMポリシー、VPC設計、ALB、Route 53、CloudFront、Lambda、DynamoDB、CloudTrail、Configを学びます。

## 32.3 実務構築

実務構築では、ECS、Fargate、CI/CD、IaC、Secrets Manager、KMS、Systems Manager、AWS Backupを学びます。

## 32.4 運用改善

運用改善では、CloudWatch、X-Ray、Security Hub、GuardDuty、Cost Explorer、Compute Optimizer、Well-Architected Toolを使います。

## 32.5 職種別の次の学習

インフラエンジニアは、VPC、Direct Connect、Transit Gateway、Organizations、Control Tower、IaCを深めます。

アプリケーションエンジニアは、Lambda、ECS、API Gateway、DynamoDB、SQS、EventBridge、CI/CDを深めます。

セキュリティエンジニアは、IAM、KMS、GuardDuty、Security Hub、Inspector、Macie、CloudTrail、Configを深めます。

SREは、CloudWatch、X-Ray、Auto Scaling、障害対応、信頼性設計、Well-Architectedを深めます。

データエンジニアは、S3、Glue、Athena、Redshift、Kinesis、Lake Formationを深めます。

AI/MLエンジニアは、Bedrock、SageMaker AI、データ基盤、MLOps、AIセキュリティを深めます。

## 32.6 AWS認定資格

最初の資格としては、AWS Certified Cloud PractitionerまたはAWS Certified Solutions Architect - Associateが候補になります。

資格は目的ではなく、知識の抜け漏れを確認する手段です。ハンズオンと設計説明を組み合わせて学ぶと実務力につながります。

---

# 付録A AWS重要用語集

![付録A AWS重要用語集](/images/aws-study/fig_035_aws.png)


- アカウント：AWS利用の契約・管理単位です。
- ARN：AWSリソースを一意に表す名前です。
- リージョン：AWSリソースを配置する地理的地域です。
- AZ：リージョン内の独立した設備群です。
- VPC：AWS上の仮想ネットワークです。
- CIDR：IPアドレス範囲を表す記法です。
- サブネット：VPCを分割したIP範囲です。
- セキュリティグループ：リソース単位の仮想ファイアウォールです。
- IAM：認証と認可を管理するサービスです。
- ロール：一時的に引き受ける権限です。
- ポリシー：許可や拒否を定義するJSONです。
- KMS：暗号鍵を管理するサービスです。
- S3：オブジェクトストレージです。
- EBS：EC2向けブロックストレージです。
- RDS：マネージドRDBサービスです。
- DynamoDB：マネージドNoSQLデータベースです。
- Lambda：イベントでコードを実行するサーバーレスサービスです。
- CloudWatch：メトリクスとログの監視サービスです。
- CloudTrail：AWS API操作の監査ログサービスです。
- IaC：インフラをコードで管理する考え方です。
- DR：災害復旧です。
- RTO：復旧までに許容される時間です。
- RPO：許容されるデータ損失時点です。

---

# 付録B よく使うAWS CLIコマンド集

![付録B よく使うAWS CLIコマンド集](/images/aws-study/fig_036_aws.png)


```bash
# 現在の認証主体を確認
aws sts get-caller-identity

# CLI設定を確認
aws configure list

# S3バケット一覧
aws s3 ls

# EC2一覧
aws ec2 describe-instances

# VPC一覧
aws ec2 describe-vpcs

# RDS一覧
aws rds describe-db-instances

# Lambda一覧
aws lambda list-functions

# CloudWatch Logsロググループ一覧
aws logs describe-log-groups

# CloudTrailイベント検索
aws cloudtrail lookup-events

# CloudFormationスタック一覧
aws cloudformation list-stacks
```

---

# 付録C IAMポリシー例

![付録C IAMポリシー例](/images/aws-study/fig_037_iam.png)


## S3読み取り専用

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::example-bucket",
        "arn:aws:s3:::example-bucket/*"
      ]
    }
  ]
}
```

## 明示的Denyの例

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "s3:DeleteObject",
      "Resource": "arn:aws:s3:::example-bucket/*"
    }
  ]
}
```

明示的DenyはAllowより優先されます。削除を絶対に防ぎたい場合などに使います。

---

# 付録D セキュリティチェックリスト

![付録D セキュリティチェックリスト](/images/aws-study/fig_038_security.png)


- ルートユーザーにMFAを設定していますか。
- ルートユーザーを日常作業に使っていませんか。
- 管理者権限を持つ利用者を把握していますか。
- 未使用アクセスキーを削除していますか。
- S3バケットの公開設定を確認していますか。
- CloudTrailを有効化していますか。
- GuardDutyを有効化していますか。
- Security Hubで検出結果を集約していますか。
- 重要データをKMSで暗号化していますか。
- Secrets ManagerやParameter Storeで機密情報を管理していますか。
- セキュリティグループでSSHやRDPを全開放していませんか。
- バックアップと復元テストを行っていますか。
- CloudWatchアラームを設定していますか。
- 予算アラートを設定していますか。

---

# 付録E コスト最適化チェックリスト

![付録E コスト最適化チェックリスト](/images/aws-study/fig_039_cost.png)


- AWS Budgetsを設定していますか。
- Cost Explorerでサービス別コストを確認していますか。
- タグでコスト配分できていますか。
- 未使用EC2を停止または削除していますか。
- 未使用EBSを削除していますか。
- 古いスナップショットを確認していますか。
- NAT Gatewayの利用状況を確認していますか。
- S3ライフサイクルを設定していますか。
- RDSサイズを見直していますか。
- Savings Plansを検討していますか。
- Spot利用可能な処理を検討していますか。
- CloudWatch Logsの保持期間を設定していますか。
- 開発環境を夜間停止できますか。
- データ転送料を確認していますか。

---

# 付録F トラブルシューティング早見表

![付録F トラブルシューティング早見表](/images/aws-study/fig_040_troubleshooting.png)


| 事象 | 最初に確認すること | 関連サービス |
|---|---|---|
| EC2に接続できない | SG、NACL、ルート、鍵、Session Manager | EC2、VPC、SSM |
| ALBで502が出る | ターゲット状態、ポート、アプリログ | ALB、EC2、ECS |
| RDSに接続できない | SG、サブネット、認証情報、DB状態 | RDS、VPC |
| Lambdaがタイムアウトする | 外部接続、VPC、NAT、DNS、メモリ | Lambda、VPC |
| S3でAccessDenied | IAM、バケットポリシー、KMS、Block Public Access | S3、IAM、KMS |
| CloudFrontで古い内容 | キャッシュ、Invalidation、Cache-Control | CloudFront、S3 |
| コストが急増した | サービス別、リージョン別、タグ別に確認 | Cost Explorer |

---

# 最終まとめ

![最終まとめ](/images/aws-study/fig_041_aws_learning.png)


AWSを理解するうえで最も重要なのは、個別サービスを断片的に覚えることではありません。**IAMで権限を制御し、VPCで通信を設計し、マネージドサービスで運用負担を下げ、CloudWatchとCloudTrailで状態を観測し、IaCで再現可能にし、Well-Architectedで継続的に改善すること**です。

AWSは、学習範囲が広いサービスです。しかし、基礎の考え方は一貫しています。何を守るのか、どこに置くのか、どう通信するのか、どう止まりにくくするのか、どう監視するのか、どうコストを抑えるのか。この問いに答えられるようになると、サービス名の暗記ではなく、実務で使えるAWS設計力が身につきます。

---

[前編へ戻る](/articles/aws-study)
