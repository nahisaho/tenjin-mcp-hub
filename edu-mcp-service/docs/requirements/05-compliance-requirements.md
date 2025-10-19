# コンプライアンス要件詳細定義書

**作成日**: 2025年10月19日  
**プロジェクト**: Tenjin MCP Hub  
**ドキュメントタイプ**: Compliance Requirements Document (CRD)  
**バージョン**: 1.0  

## 1. 概要

本文書では、教育機関向けマルチベンダーMCPサービスが準拠すべき法的・規制要件を詳細に定義します。教育データ保護、プライバシー規制、セキュリティ標準、国際規格への準拠要件を包括的に規定し、グローバルな教育市場での法的適合性を確保します。

### 1.1 コンプライアンス要件カテゴリ
- **CR-PRIVACY**: プライバシー・データ保護規制
- **CR-EDUCATION**: 教育固有規制・標準
- **CR-SECURITY**: セキュリティ・情報保護標準
- **CR-BUSINESS**: 事業規制・商取引法

## 2. CR-PRIVACY: プライバシー・データ保護規制

### 2.1 EU一般データ保護規則（GDPR）準拠

#### CR-PRIVACY-001: GDPR基本原則準拠
**優先度**: P0  
**規制**: EU GDPR (2016/679)  
**適用範囲**: EU域内データ主体、EU域内データ処理  
**準拠要件**:
- **適法性（Lawfulness）**: 処理の法的根拠明確化
- **公正性（Fairness）**: データ主体に対する公正な処理
- **透明性（Transparency）**: 処理目的・方法の明確な説明
- **目的制限（Purpose limitation）**: 収集目的に限定した利用
- **データ最小化（Data minimisation）**: 必要最小限のデータ収集
- **正確性（Accuracy）**: データの正確性維持・更新
- **保存制限（Storage limitation）**: 適切な保存期間設定
- **完全性・機密性（Integrity and confidentiality）**: 技術的・組織的保護措置

**実装要件**:
```json
{
  "data_processing_record": {
    "controller": "Educational MCP Platform Ltd.",
    "purposes": ["educational_service_provision", "learning_analytics"],
    "legal_basis": "consent",
    "categories_of_data": ["personal_identifiers", "educational_records"],
    "recipients": ["content_providers", "analytics_processors"],
    "transfers": {
      "third_countries": ["US", "JP"],
      "safeguards": "adequacy_decision"
    },
    "retention_period": "7_years_post_graduation",
    "technical_measures": ["encryption", "access_controls", "audit_logging"]
  }
}
```

#### CR-PRIVACY-002: データ主体の権利実装
**優先度**: P0  
**準拠権利**:
- **情報提供権（Right to be informed）**: プライバシー通知の提供
- **アクセス権（Right of access）**: 個人データへのアクセス提供
- **訂正権（Right to rectification）**: 不正確データの訂正
- **削除権（Right to erasure）**: データの削除（忘れられる権利）
- **処理制限権（Right to restrict processing）**: 処理の制限
- **データポータビリティ権（Right to data portability）**: データの転送可能性
- **異議申立権（Right to object）**: 処理への異議申立
- **自動決定に関する権利**: プロファイリング・自動決定への保護

**実装要件**:
- 権利行使ポータルの提供（30日以内対応）
- 身元確認プロセスの実装
- データエクスポート機能（JSON/CSV形式）
- 削除影響範囲の自動分析
- 処理制限フラグの実装
- 権利行使ログの保持

#### CR-PRIVACY-003: 同意管理システム
**優先度**: P0  
**要件仕様**:
- **明確な同意（Clear consent）**: 具体的・明確な同意取得
- **自由な同意（Freely given）**: 強制されない同意
- **特定の同意（Specific consent）**: 処理目的別の同意
- **事前の同意（Informed consent）**: 十分な情報提供後の同意
- **撤回可能性（Withdrawable）**: 同意撤回の容易さ

**実装要件**:
```javascript
// 同意管理システム実装例
const consentManagement = {
  granularConsent: {
    essential: true,  // 必須機能（同意不要）
    analytics: false, // 学習分析（同意必要）
    marketing: false, // マーケティング（同意必要）
    thirdParty: false // 第三者データ共有（同意必要）
  },
  consentRecord: {
    timestamp: "2025-01-15T10:30:00Z",
    ipAddress: "192.168.1.100",
    userAgent: "Mozilla/5.0...",
    method: "explicit_checkbox",
    purposes: ["educational_service", "learning_analytics"],
    retention: "7_years"
  },
  withdrawalMechanism: {
    method: "privacy_dashboard",
    effect: "immediate",
    notification: true
  }
}
```

### 2.2 カリフォルニア州消費者プライバシー法（CCPA）準拠

#### CR-PRIVACY-004: CCPA消費者権利実装
**優先度**: P1  
**規制**: California Consumer Privacy Act (CCPA/CPRA)  
**適用範囲**: カリフォルニア州居住者  
**準拠要件**:
- **知る権利（Right to Know）**: 個人情報の収集・利用・共有の開示
- **削除権（Right to Delete）**: 個人情報の削除要求
- **売却拒否権（Right to Opt-Out）**: 個人情報売却の拒否
- **サービス拒否禁止（Non-Discrimination）**: 権利行使による差別的取扱の禁止

**実装要件**:
- カリフォルニア州居住者判定機能
- CCPA準拠プライバシー通知
- "Do Not Sell My Personal Information"リンク
- 売却・共有データの追跡システム
- 差別的取扱防止ポリシー

### 2.3 その他主要プライバシー規制

#### CR-PRIVACY-005: 多国籍プライバシー法準拠
**優先度**: P1  
**対象規制**:
- **カナダ PIPEDA**: Personal Information Protection and Electronic Documents Act
- **日本 個人情報保護法**: Personal Information Protection Act
- **ブラジル LGPD**: Lei Geral de Proteção de Dados
- **オーストラリア Privacy Act**: Privacy Act 1988

**実装要件**:
- 地域別プライバシー通知の提供
- データローカライゼーション要件への対応
- 越境データ転送時の適切な保護措置
- 地域別データ保護責任者（DPO）の任命

## 3. CR-EDUCATION: 教育固有規制・標準

### 3.1 米国家族教育権・プライバシー法（FERPA）準拠

#### CR-EDUCATION-001: FERPA基本要件準拠
**優先度**: P0  
**規制**: Family Educational Rights and Privacy Act (20 U.S.C. § 1232g)  
**適用範囲**: 米国連邦資金受給教育機関  
**準拠要件**:
- **教育記録の定義**: 学生個人識別可能な教育記録の適切な管理
- **親・学生の権利**: 18歳未満は親、18歳以上は学生の同意権
- **開示制限**: 法定例外以外の第三者開示禁止
- **ディレクトリ情報**: 公開可能情報の事前通知・オプトアウト

**実装要件**:
```json
{
  "ferpa_compliance": {
    "education_records": {
      "definition": "personally_identifiable_student_records",
      "scope": ["grades", "transcripts", "course_enrollments", "disciplinary_records"],
      "exclusions": ["sole_possession_notes", "law_enforcement_records", "employment_records"]
    },
    "consent_management": {
      "age_threshold": 18,
      "parental_consent": "required_under_18",
      "student_consent": "required_18_and_over",
      "consent_verification": "digital_signature_required"
    },
    "disclosure_controls": {
      "legitimate_educational_interest": true,
      "directory_information": {
        "opt_out_period": "14_days_annual_notice",
        "included_fields": ["name", "email", "enrollment_status", "graduation_date"]
      },
      "audit_trail": "complete_disclosure_logging"
    }
  }
}
```

#### CR-EDUCATION-002: FERPA例外規定適用
**優先度**: P0  
**法定例外**:
- **学校職員**: 正当な教育的利益を有する職員への開示
- **転校**: 学生の転校先教育機関への記録転送
- **監査**: 政府機関による監査・評価
- **財政援助**: 学資援助プログラムでの開示
- **研究**: 統計目的での匿名化研究利用
- **緊急事態**: 健康・安全緊急事態での開示

**実装要件**:
- 例外事由別の自動判定システム
- 職員アクセス権限の厳格管理
- 転校時の安全な記録転送プロトコル
- 監査機関への限定的データ提供機能
- 緊急事態対応プロトコル

### 3.2 児童オンラインプライバシー保護法（COPPA）準拠

#### CR-EDUCATION-003: COPPA年齢認証・同意システム
**優先度**: P0  
**規制**: Children's Online Privacy Protection Act (15 U.S.C. §§ 6501-6506)  
**適用範囲**: 13歳未満児童対象サービス  
**準拠要件**:
- **年齢認証**: 13歳未満ユーザーの確実な識別
- **保護者同意**: 検証可能な保護者同意の取得
- **データ最小化**: 必要最小限の情報収集
- **保護者権利**: アクセス、削除、情報変更権の提供
- **データ保護**: 適切なセキュリティ措置の実装

**実装要件**:
```javascript
// COPPA準拠年齢認証システム
const coppaCompliance = {
  ageVerification: {
    methods: ["birth_date_input", "grade_level_validation", "school_verification"],
    threshold: 13,
    verification_required: true
  },
  parentalConsent: {
    methods: [
      "credit_card_verification",
      "signed_email_consent", 
      "postal_mail_consent",
      "toll_free_phone_verification"
    ],
    verification_level: "enhanced",
    retention_period: "consent_duration_plus_reasonable_period"
  },
  dataMinimization: {
    essential_only: true,
    behavioral_advertising: false,
    location_services: false,
    social_features: "limited"
  },
  parentalRights: {
    review_child_info: true,
    delete_child_info: true,
    refuse_further_collection: true,
    opt_out_communications: true
  }
}
```

#### CR-EDUCATION-004: 教育技術プライバシー標準
**優先度**: P1  
**標準**: Student Data Privacy Consortium (SDPC)  
**準拠要件**:
- **Student Privacy Pledge**: 学生プライバシー誓約の遵守
- **EdTech Privacy Standards**: 教育技術プライバシー標準準拠
- **Data Governance**: 学生データガバナンス体制の構築
- **Vendor Assessment**: ベンダー評価・選定プロセスの実装

## 4. CR-SECURITY: セキュリティ・情報保護標準

### 4.1 SOC 2 Type II準拠

#### CR-SECURITY-001: SOC 2信頼サービス基準
**優先度**: P0  
**標準**: AICPA SOC 2 Type II  
**信頼サービス基準**:
- **セキュリティ（Security）**: 情報・システムの不正アクセス防止
- **可用性（Availability）**: システム・サービスの運用可用性
- **処理の完全性（Processing Integrity）**: 処理の完全性・正確性
- **機密性（Confidentiality）**: 機密情報の保護
- **プライバシー（Privacy）**: 個人情報の収集・利用・保持・開示・廃棄

**実装要件**:
```yaml
# SOC 2 Control Framework
soc2_controls:
  security:
    CC6.1: # Logical and Physical Access Controls
      - multi_factor_authentication
      - role_based_access_control
      - privileged_access_management
      - physical_datacenter_security
    CC6.2: # System Software Management
      - patch_management
      - vulnerability_scanning
      - change_management
      - configuration_management
    CC6.3: # Data Protection
      - encryption_at_rest
      - encryption_in_transit
      - key_management
      - data_classification
  availability:
    CC7.1: # System Capacity
      - capacity_planning
      - performance_monitoring
      - auto_scaling
      - load_balancing
    CC7.2: # System Recovery
      - backup_procedures
      - disaster_recovery
      - business_continuity
      - rto_rpo_targets
  processing_integrity:
    CC8.1: # Data Processing
      - input_validation
      - output_verification
      - error_handling
      - processing_controls
```

#### CR-SECURITY-002: ISO 27001情報セキュリティ管理
**優先度**: P1  
**標準**: ISO/IEC 27001:2022  
**要件カテゴリ**:
- **情報セキュリティポリシー**: 組織レベルのセキュリティ方針
- **情報セキュリティ組織**: セキュリティ管理体制
- **人的資源セキュリティ**: 従業員セキュリティ管理
- **資産管理**: 情報資産の分類・管理
- **アクセス制御**: システム・情報へのアクセス制御
- **暗号化**: 暗号技術の適切な利用
- **物理的・環境的セキュリティ**: 物理的保護措置
- **運用セキュリティ**: 日常的セキュリティ運用
- **通信セキュリティ**: ネットワーク・通信保護
- **システム取得・開発・保守**: 開発ライフサイクルセキュリティ
- **供給者関係**: サプライチェーンセキュリティ
- **情報セキュリティインシデント管理**: インシデント対応
- **事業継続性**: 事業継続・災害復旧
- **コンプライアンス**: 法的・規制要件準拠

### 4.2 NIST Cybersecurity Framework準拠

#### CR-SECURITY-003: NIST CSF実装
**優先度**: P1  
**フレームワーク**: NIST Cybersecurity Framework 2.0  
**機能（Functions）**:
- **特定（Identify）**: 資産・リスクの特定
- **保護（Protect）**: 保護対策の実装
- **検出（Detect）**: セキュリティ事象の検出
- **対応（Respond）**: インシデント対応
- **復旧（Recover）**: 復旧・改善
- **統制（Govern）**: ガバナンス・リスク管理

**実装要件**:
```python
# NIST CSF Implementation Matrix
nist_csf_controls = {
    "identify": {
        "ID.AM": "Asset Management",
        "ID.BE": "Business Environment",
        "ID.GV": "Governance",
        "ID.RA": "Risk Assessment",
        "ID.RM": "Risk Management Strategy",
        "ID.SC": "Supply Chain Risk Management"
    },
    "protect": {
        "PR.AC": "Identity Management and Access Control",
        "PR.AT": "Awareness and Training",
        "PR.DS": "Data Security",
        "PR.IP": "Information Protection Processes",
        "PR.MA": "Maintenance",
        "PR.PT": "Protective Technology"
    },
    "detect": {
        "DE.AE": "Anomalies and Events",
        "DE.CM": "Security Continuous Monitoring",
        "DE.DP": "Detection Processes"
    },
    "respond": {
        "RS.RP": "Response Planning",
        "RS.CO": "Communications",
        "RS.AN": "Analysis",
        "RS.MI": "Mitigation",
        "RS.IM": "Improvements"
    },
    "recover": {
        "RC.RP": "Recovery Planning",
        "RC.IM": "Improvements",
        "RC.CO": "Communications"
    }
}
```

### 4.3 FedRAMP準拠（将来要件）

#### CR-SECURITY-004: FedRAMP認証対応
**優先度**: P2  
**標準**: Federal Risk and Authorization Management Program  
**セキュリティレベル**: Moderate Impact Level  
**要件概要**:
- **NIST SP 800-53**: セキュリティコントロールベースライン
- **境界保護**: ネットワーク境界セキュリティ
- **継続監視**: 24/7セキュリティ監視
- **インシデント対応**: 連邦政府標準の対応手順
- **認証機関**: 第三者評価機関（3PAO）による評価

## 5. CR-BUSINESS: 事業規制・商取引法

### 5.1 アクセシビリティ規制準拠

#### CR-BUSINESS-001: 米国障害者法（ADA）準拠
**優先度**: P0  
**規制**: Americans with Disabilities Act (ADA)  
**準拠標準**: WCAG 2.1 AA  
**要件領域**:
- **知覚可能性（Perceivable）**: 代替テキスト、キャプション、色に依存しない設計
- **操作可能性（Operable）**: キーボード操作、発作誘発防止、操作時間制限
- **理解可能性（Understandable）**: 読みやすさ、予測可能性、入力支援
- **堅牢性（Robust）**: 支援技術との互換性

**実装要件**:
```html
<!-- アクセシビリティ実装例 -->
<div role="main" aria-labelledby="course-title">
  <h1 id="course-title">機械学習入門コース</h1>
  
  <video controls aria-describedby="video-desc">
    <source src="lecture1.mp4" type="video/mp4">
    <track kind="captions" src="lecture1-captions.vtt" srclang="ja" label="日本語">
    <track kind="descriptions" src="lecture1-descriptions.vtt" srclang="ja" label="音声解説">
  </video>
  
  <div id="video-desc">
    この講義では機械学習の基本概念について説明します。
  </div>
  
  <form role="form" aria-labelledby="quiz-title">
    <h2 id="quiz-title">理解度チェック</h2>
    <fieldset>
      <legend>質問1: 機械学習の定義として正しいものは？</legend>
      <label><input type="radio" name="q1" value="a" aria-describedby="q1-a-desc">
        コンピューターが明示的にプログラムされることなく学習する能力
      </label>
      <div id="q1-a-desc" class="sr-only">正解です</div>
    </fieldset>
  </form>
</div>
```

#### CR-BUSINESS-002: 欧州アクセシビリティ法準拠
**優先度**: P1  
**規制**: European Accessibility Act (EAA)  
**標準**: EN 301 549 V3.2.1  
**適用範囲**: EU域内での電子商取引サービス  
**要件**:
- パソコン・モバイル両対応のアクセシビリティ
- 音声・映像コンテンツの字幕・手話対応
- 認知障害者向けの理解しやすいインターフェース
- 支援技術との完全互換性

### 5.2 消費者保護法準拠

#### CR-BUSINESS-003: オンライン契約法準拠
**優先度**: P0  
**適用法域**: 
- **米国**: Electronic Signatures in Global and National Commerce Act (E-SIGN)
- **EU**: eIDAS Regulation
- **日本**: 電子署名法
- **カナダ**: Electronic Transactions Protection Act

**実装要件**:
- 明確な利用規約・プライバシーポリシー
- 電子署名・同意の法的有効性確保
- クーリングオフ期間の適切な設定
- 自動更新契約の明確な通知
- 料金・課金条件の透明性

#### CR-BUSINESS-004: 国際税務・関税法準拠
**優先度**: P1  
**対象領域**:
- **デジタルサービス税**: EU Digital Services Act準拠
- **VAT/消費税**: 販売地点での適切な税率適用
- **源泉税**: 国際サービス提供での源泉税処理
- **移転価格**: 関連会社間取引の適正価格設定

**実装要件**:
```json
{
  "tax_compliance": {
    "vat_calculation": {
      "eu_rules": "destination_principle",
      "threshold": "10000_eur_annual",
      "moss_registration": "required_for_b2c",
      "rates": {
        "DE": 0.19,
        "FR": 0.20,
        "UK": 0.20,
        "US": "state_dependent",
        "JP": 0.10
      }
    },
    "digital_services_tax": {
      "threshold": "750m_eur_global_revenue",
      "applicable_countries": ["FR", "UK", "IT", "ES"],
      "rate": "3_percent_local_revenue"
    },
    "transfer_pricing": {
      "documentation": "master_file_local_file",
      "arm_length_principle": true,
      "advance_pricing_agreement": "recommended"
    }
  }
}
```

## 6. 地域別特殊要件

### 6.1 アジア太平洋地域

#### CR-REGION-001: 中国データローカライゼーション
**優先度**: P2  
**規制**: 中国網路安全法（Cybersecurity Law）  
**要件**:
- 個人情報・重要データの中国国内保存
- データ国外移転時の安全評価
- ネットワークセキュリティレベル保護制度準拠
- 政府機関への情報提供協力義務

#### CR-REGION-002: シンガポール個人データ保護法
**優先度**: P2  
**規制**: Personal Data Protection Act (PDPA)  
**要件**:
- 個人データの同意ベース収集・利用
- データ漏洩通知義務（72時間以内）
- データ保護責任者（DPO）の任命
- 国外データ移転時の適切な保護措置

### 6.2 中東・アフリカ地域

#### CR-REGION-003: UAE データ保護法
**優先度**: P2  
**規制**: UAE Federal Decree-Law No. 45 of 2021  
**要件**:
- 健康・遺伝データの特別保護
- 機密データの国内処理義務
- データ主体の包括的権利保障
- サイバーセキュリティ委員会への報告義務

## 7. コンプライアンス管理体制

### 7.1 ガバナンス構造

#### CR-GOVERNANCE-001: プライバシーガバナンス
**実装要件**:
- **最高プライバシー責任者（CPO）**: プライバシー戦略・方針策定
- **データ保護責任者（DPO）**: GDPR準拠監督・助言
- **プライバシー委員会**: 多部門横断の意思決定機関
- **地域別プライバシー担当者**: 各地域法令への個別対応

#### CR-GOVERNANCE-002: コンプライアンス監視
**実装システム**:
```python
# コンプライアンス監視システム
class ComplianceMonitoring:
    def __init__(self):
        self.frameworks = [
            "GDPR", "CCPA", "FERPA", "COPPA", 
            "SOC2", "ISO27001", "NIST_CSF"
        ]
        self.monitoring_frequency = "continuous"
        
    def compliance_dashboard(self):
        return {
            "overall_score": 0.95,
            "risk_levels": {
                "high": 2,
                "medium": 8,
                "low": 15
            },
            "recent_audits": [
                {
                    "framework": "SOC2_TypeII",
                    "date": "2025-01-15",
                    "result": "passed",
                    "recommendations": 3
                }
            ],
            "upcoming_requirements": [
                {
                    "regulation": "EU_AI_Act",
                    "effective_date": "2025-08-01",
                    "impact": "medium",
                    "preparation_status": "in_progress"
                }
            ]
        }
```

### 7.2 継続的コンプライアンス

#### CR-GOVERNANCE-003: 法的要件追跡システム
**機能要件**:
- 法令変更の自動監視・通知
- 影響度評価・対応計画策定
- コンプライアンス教育・訓練管理
- 内部監査・第三者監査管理
- 是正措置・改善計画追跡

**実装アーキテクチャ**:
- 法的情報データベース（定期更新）
- 影響度分析エンジン
- 対応計画管理システム
- 監査証跡管理
- レポーティング・ダッシュボード

## 8. コンプライアンス証明・監査

### 8.1 第三者認証・監査

#### CR-AUDIT-001: 定期監査スケジュール
**監査計画**:
- **SOC 2 Type II**: 年次監査（外部監査法人）
- **ISO 27001**: 年次監査（認証機関）
- **プライバシー監査**: 四半期内部監査
- **脆弱性評価**: 月次外部評価
- **ペネトレーションテスト**: 年2回

#### CR-AUDIT-002: 監査証跡管理
**要件**:
- 完全な操作ログ保持（最低7年間）
- 改ざん防止機能（デジタル署名・ハッシュ）
- 検索・分析機能
- 法執行機関対応機能
- プライバシー配慮ログ生成

## 9. 新興規制対応

### 9.1 AI・機械学習規制

#### CR-EMERGING-001: EU AI法対応準備
**規制**: EU Artificial Intelligence Act  
**施行予定**: 2025年8月  
**影響範囲**: 高リスクAIシステム  
**準備要件**:
- AIシステムのリスク分類
- 高リスクシステムの適合性評価
- CE マーキング・EU適合宣言
- 品質管理システム構築
- 透明性・説明可能性確保

#### CR-EMERGING-002: アルゴリズムの説明責任
**適用領域**: 自動化された意思決定システム  
**要件**:
- アルゴリズム動作の透明性
- バイアス検出・軽減措置
- 人間による監督・介入機能
- 影響を受ける個人への説明提供
- 定期的なアルゴリズム監査

---

**承認者署名欄**:
- 最高プライバシー責任者（CPO）: ________________
- 法務責任者（CLO）: ________________  
- 最高技術責任者（CTO）: ________________  
- 承認日: ________________

**関連文書**:
- [要件定義書概要](00-requirements-overview.md)
- [機能要件詳細定義書](02-functional-requirements.md)
- [非機能要件詳細定義書](03-non-functional-requirements.md)
- [ソフトウェア要件詳細定義書](04-software-requirements.md)
- [要件トレーサビリティマトリックス](01-requirements-traceability-matrix.md)