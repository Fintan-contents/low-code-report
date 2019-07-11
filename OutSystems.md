﻿## OutSystemsの製品評価

OutSystemsはポルトガルのOutSystems社が提供するローコード開発基盤です。  
OutSystems Service Studioという専用の開発ツールを使用して、ビジュアルなモデルを記述することで、動作するアプリケーションを開発できます。  

<img src="https://github.com/Fintan-contents/low-code-report/blob/master/img/OutSystems_Image1.png?raw=true" alt="業務アプリを表現するモデル" width="722px">

OutSystemsでは開発・実行環境が一体的に提供されており、OutSystems Service Studioから開発、試験実行、デプロイのすべてを実行できます。  
また、開発および実行環境についてはクラウド／オンプレミスの両方に対応しており、特にOutSystems社から提供されているパブリッククラウド環境を利用する場合、すぐにアプリの開発～公開が可能となります。  

### モデリング言語
OutSystemsでは、アプリケーションをプロセス、インターフェース、ロジック、データの4つのモデルにより表現しています。  


|OutSystemsにおけるモデルの要素|説明|
|:---|:---|
|プロセス|ワークフローやタイマー（バッチ）のように画面操作から離れて実行されるビジネスプロセスを実装する。|
|インターフェース|画面および画面遷移と各画面における処理を実装する。|
|ロジック|画面やデータベースに紐づく処理、それらと紐づかない個別の処理や、外部システムとのインターフェースを実装する。|
|データ|テーブル定義とテーブル単位のデータベースに対する単純なCRUD処理を実装する。|

### モデル駆動開発
OutSystemsではデータベースを起点とした自動生成機能により画面の主要機能をモデルとして自動生成したのち、GUIベースのツールによりビジュアルなモデルを追記してゆくことでアプリケーションを完成させます。  

#### 自動生成機能
OutSystemsではテーブル定義から、以下の処理を自動生成する機能があります。  
* テーブルに対する単純なCRUDのためのデータベース処理。  
* テーブルに対する一覧画面と閲覧編集のための詳細画面と基本的な処理。  

各画面には以下の機能が含まれているので、単純なマスタメンテ画面であれば自動生成されたものがそのまま利用できます。  
* 一覧画面  
テーブルの全カラムを表示する表、それに対して件数が多い時のページング、並び替えおよび検索機能が含まれています。  
* 詳細画面  
テーブルの全項目の表示、新規追加、更新、削除および、データモデルに設定したデータ型に対して矛盾するデータを登録できないようにするバリデーション機能が含まれています。  

#### インターフェースにおけるウィジェット内部処理の見える化
OutSystemsでは画面の構成部品であるウィジェットのデータベースアクセスなどの内部処理が、アクションフローとして見える化されます。  

以下のアクションフローは詳細画面におけるデータベースへの保存処理で、バリデーションの発動、データベースへの保存、メッセージ表示や、例外処理が見える化されています。  

<img src="https://github.com/Fintan-contents/low-code-report/blob/master/img/OutSystems_Image2.png?raw=true" alt="アクションフロー" width="570px">

上記のようなアクションフローは自動生成機能により生成されます。  
これをカスタマイズすることで、様々な付加機能を追加することができます。  

### 画面デザインの自由度
画面はOutSystemsが用意したテンプレートを使用することが基本となります。デザインコンポーネント（ウィジェット）としてToggleボタンなど、アプリケーションで多用されるUI部品が多数用意されているので、これらを組み合わせて画面をカスタマイズすることができます。  
オブジェクトの位置や装飾を変更する微調整はできますが、HTMLソースを直接修正することはできません。テンプレートにはない独自のデザインについては個別に用意したCSSにて対応します。  

### ロジック自由度と拡張性
処理ロジックはインターフェースモデル、ロジックモデル上に作成することができますが、いずれも、GUIベースのツールを用いて、フローチャート形式のアクションフローと計算式にて表現します。  
上記に加えて、DLLやC#で実装したコードを組み込むことも可能です。C#でオリジナルコンポーネントを用意してロジックを拡張したり、DLLなどの既存資産を再利用したりすることができます。  

アクションフローは分岐、ループ、サブプロセス呼び出しなどをサポートしており、一般的なプログラミング言語と同等の表現力があると推測されますが、複雑な処理の場合はアクションフローが肥大化する懸念があります。これについては、前述のC#による実装を併用することで、アクションフローをスリムに維持したままで、複雑な処理を実装することができます。  

### 製品を使用した感想
OutSystemsを使った感想について以下に記述します。  
※本章については、無料セミナーへの参加と公開資料による学習のみ実施した開発者がサンプルアプリを構築した時に感じた感想となります。3～5日間の本格的な有償トレーニングを受講した開発者の感想とは異なる場合があります。  
<table><tr><td>
OutSystemsではウィジェットのデータベースアクセスなどの内部動作がアクションフローとして見える化されるので、画面関連の処理ロジックの量は多くなる傾向があります。<br>
<br>
しかし、内部動作が把握可能なことによって、実行時の動作仕様が推測しやすいというメリットがありました。<br>
今回のサンプルアプリ構築時においても、コンポーネントなどの仕様を十分に理解していませんでしたが、アクションフローを参照することで動作仕様が推測でき、カスタマイズ方法も容易に見つけることができました。<br>
<br>
また、計算式を入力する必要があった場面においては、入力候補の補完機能だけでなく、コーディング時に参照可能なウィジェット、データモデル、変数などのオブジェクトが表示されており、クリック操作でそのオブジェクトを参照するためのコードを補完してくれました。<br>
この機能により、マニュアルの参照なしに開発を進めることができました。<br>
<br>
Javaなどの開発経験が豊富なエンジニアには、扱いやすいツールであると感じました。
</td></tr></table>


### 効果的な活用場面
OutSystemsの特徴と活用に適する場面は以下のとおりと考えます。  
* ロジック部分も含めてGUIベースのツールを用いたビジュアルなモデリングによりアプリケーションの定義が完結する。  
→デベロッパ、ユーザが共同でシステムの開発、保守に関与する場合。  
→様々な機能を作りこみたい場合。  
* ウィジェットのデータベースアクセスなどの内部処理がアクションフローとして見える化され、動作を把握しやすいので、スクラッチ開発経験者にとって親和性が高い。  
　→スクラッチ開発に慣れたエンジニア中心で開発する場合。  
* デプロイやバージョン管理なども含めてオールインワンで提供されている。  
　→新規にソースコード管理環境や、リリース運用環境を構築したい場合。  
* 契約するとすぐに利用可能となるパブリッククラウド版が提供されている。  
→手早くサービスを立ち上げたい場合。  
* 規模に応じた料金体系となっている。  
→スモールスタートして徐々に規模拡大していきたい場合。