---
title: Stripe
description: 了解如何将支付数据从Stripe帐户摄取到Adobe Experience Platform
exl-id: 191d217e-036d-491a-b7dd-abcad74625ba
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---

# [!DNL Stripe]

数千家各种规模的企业利用[!DNL Stripe]在线或亲自接受付款、创造新的收入来源，并在Adobe Experience Platform、Adobe Commerce和[!DNL Magento Open Source]的帮助下在全球范围内进行扩展。

在Experience Platform中使用[!DNL Stripe]源摄取客户在购买流程中捕获的数据。 引入后，使用此数据创建个性化优惠并解锁更丰富的业务洞察。

>[!TIP]
>
>有关Experience Platform上[!DNL Stripe]源的问题，请通过adobe-partnership[!DNL Stripe]@stripe.com联系<span>。

>[!BEGINSHADEBOX]

**源[!DNL Stripe]的示例用例**

您的企业允许客户在您的在线商店购买商品，其选项为&#x200B;**立即购买**&#x200B;和&#x200B;**稍后付款**（使用[!DNL Klarna]、[!DNL Afterpay]、[!DNL Affirm]或[!DNL Zip]）。

使用[!DNL Stripe]数据源分析&#x200B;**立即购买**&#x200B;和&#x200B;**稍后付款**&#x200B;选项的使用情况，并尝试为这些客户提供个性化优惠。 例如，考虑推荐附加产品，以便在结账前增加购物车中的产品数量。

>[!ENDSHADEBOX]

请阅读以下文档，了解如何设置[!DNL Stripe]源帐户、检索必要的凭据以及创建架构。

## 先决条件 {#prerequisites}

以下部分提供了在将[!DNL Stripe]帐户连接到Experience Platform之前必须完成的先决条件设置的信息。

### 检索您的访问令牌

* 使用您的[[!DNL Stripe] 电子邮件地址和密码登录到](https://dashboard.stripe.com/login)仪表板[!DNL Stripe]。
* 在[!DNL Developers]仪表板中，选择&#x200B;**[!DNL API keys for developers]**。
* 在&#x200B;**API密钥**&#x200B;选项卡下，选择&#x200B;**[!DNL Reveal test key]**&#x200B;以显示您的访问令牌。
* 当使用[!DNL Stripe] API或Experience Platform UI将您的[!DNL Flow Service]帐户连接到Experience Platform时，您现在可以使用此令牌作为访问令牌。

### 收集所需的凭据

为了将您的[!DNL Stripe]帐户连接到Experience Platform，您必须提供以下身份验证凭据的值：

>[!BEGINTABS]

>[!TAB API]

在使用[!DNL Stripe] API连接[!DNL Flow Service]帐户时，必须提供以下凭据。

| 凭据 | 描述 |
| --- | --- |
| `accessToken` | 您的[!DNL Stripe] OAuth 2刷新代码身份验证令牌。 |
| `connectionSpec.id` | [!DNL Stripe]源的连接规范ID。 此ID被固定为： `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`。 |

>[!TAB UI]

在使用Experience Platform用户界面连接[!DNL Stripe]帐户时，必须提供以下凭据。

| 凭据 | 描述 |
| --- | --- |
| 访问令牌 | 您的[!DNL Stripe] OAuth 2刷新代码身份验证令牌。 |

>[!ENDTABS]

有关使用[!DNL Stripe] API的更多信息，请阅读有关API密钥[[!DNL Stripe] 的](https://docs.stripe.com/keys)文档。

### 创建Experience Data Model (XDM)架构

[!DNL Stripe]源支持从以下资源路径摄取数据：

* 费用
* 订阅
* 退款
* 余额交易记录
* 客户
* 价格

您必须创建描述数据集的XDM架构，该数据集可以存储将从[!DNL Stripe]发送到Experience Platform的字段和数据类型。

>[!BEGINTABS]

>[!TAB 费用]

在[!DNL Stripe]中，**费用**&#x200B;表示尝试将资金转入[!DNL Stripe]。 有关特定收费属性的更多信息，请阅读[[!DNL Stripe] 收费的API指南](https://docs.stripe.com/api/charges)。

+++选择以查看Stripe Charge对象  

```json
{
  "id": "ch_3MmlLrLkdIwHu7ix0snN0B15",
  "object": "charge",
  "amount": 1099,
  "amount_captured": 1099,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_3MmlLrLkdIwHu7ix0uke3Ezy",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null
  },
  "calculated_statement_descriptor": "Stripe",
  "captured": true,
  "created": 1679090539,
  "currency": "usd",
  "customer": null,
  "description": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "outcome": {
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "normal",
    "risk_score": 32,
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": "card_1MmlLrLkdIwHu7ixIJwEWSNR",
  "payment_method_details": {
    "card": {
      "brand": "visa",
      "checks": {
        "address_line1_check": null,
        "address_postal_code_check": null,
        "cvc_check": null
      },
      "country": "US",
      "exp_month": 3,
      "exp_year": 2024,
      "fingerprint": "mToisGZ01V71BCos",
      "funding": "credit",
      "installments": null,
      "last4": "4242",
      "mandate": null,
      "network": "visa",
      "three_d_secure": null,
      "wallet": null
    },
    "type": "card"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xTTJKVGtMa2RJd0h1N2l4KOvG06AGMgZfBXyr1aw6LBa9vaaSRWU96d8qBwz9z2J_CObiV_H2-e8RezSK_sw0KISesp4czsOUlVKY",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source_transfer": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

+++

>[!TAB 订阅]

在[!DNL Stripe]中，您可以使用&#x200B;**订阅**&#x200B;定期向客户收费。 有关特定订阅属性的更多信息，请阅读订阅[[!DNL Stripe] 上的](https://docs.stripe.com/api/subscriptions)API指南。

+++选择以查看Stripe订阅对象

```json
{
  "id": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
  "object": "subscription",
  "application": null,
  "application_fee_percent": null,
  "automatic_tax": {
    "enabled": false,
    "liability": null
  },
  "billing_cycle_anchor": 1679609767,
  "billing_thresholds": null,
  "cancel_at": null,
  "cancel_at_period_end": false,
  "canceled_at": null,
  "cancellation_details": {
    "comment": null,
    "feedback": null,
    "reason": null
  },
  "collection_method": "charge_automatically",
  "created": 1679609767,
  "currency": "usd",
  "current_period_end": 1682288167,
  "current_period_start": 1679609767,
  "customer": "cus_Na6dX7aXxi11N4",
  "days_until_due": null,
  "default_payment_method": null,
  "default_source": null,
  "default_tax_rates": [],
  "description": null,
  "discount": null,
  "ended_at": null,
  "invoice_settings": {
    "issuer": {
      "type": "self"
    }
  },
  "items": {
    "object": "list",
    "data": [
      {
        "id": "si_Na6dzxczY5fwHx",
        "object": "subscription_item",
        "billing_thresholds": null,
        "created": 1679609768,
        "metadata": {},
        "plan": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "plan",
          "active": true,
          "aggregate_usage": null,
          "amount": 1000,
          "amount_decimal": "1000",
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "interval": "month",
          "interval_count": 1,
          "livemode": false,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "tiers_mode": null,
          "transform_usage": null,
          "trial_period_days": null,
          "usage_type": "licensed"
        },
        "price": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "price",
          "active": true,
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "custom_unit_amount": null,
          "livemode": false,
          "lookup_key": null,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "recurring": {
            "aggregate_usage": null,
            "interval": "month",
            "interval_count": 1,
            "trial_period_days": null,
            "usage_type": "licensed"
          },
          "tax_behavior": "unspecified",
          "tiers_mode": null,
          "transform_quantity": null,
          "type": "recurring",
          "unit_amount": 1000,
          "unit_amount_decimal": "1000"
        },
        "quantity": 1,
        "subscription": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
        "tax_rates": []
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/subscription_items?subscription=sub_1MowQVLkdIwHu7ixeRlqHVzs"
  },
  "latest_invoice": "in_1MowQWLkdIwHu7ixuzkSPfKd",
  "livemode": false,
  "metadata": {},
  "next_pending_invoice_item_invoice": null,
  "on_behalf_of": null,
  "pause_collection": null,
  "payment_settings": {
    "payment_method_options": null,
    "payment_method_types": null,
    "save_default_payment_method": "off"
  },
  "pending_invoice_item_interval": null,
  "pending_setup_intent": null,
  "pending_update": null,
  "quantity": 1,
  "schedule": null,
  "start_date": 1679609767,
  "status": "active",
  "test_clock": null,
  "transfer_data": null,
  "trial_end": null,
  "trial_settings": {
    "end_behavior": {
      "missing_payment_method": "create_invoice"
    }
  },
  "trial_start": null
}
```

+++

>[!TAB 退款]

在[!DNL Stripe]中，您可以使用&#x200B;**退款**&#x200B;退款以前创建的费用。 有关特定退款属性的更多信息，请阅读退款[[!DNL Stripe] API指南](https://docs.stripe.com/api/refunds)。

+++选择以查看Stripe退款对象

```json
{
  "id": "re_1Nispe2eZvKYlo2Cd31jOCgZ",
  "object": "refund",
  "amount": 1000,
  "balance_transaction": "txn_1Nispe2eZvKYlo2CYezqFhEx",
  "charge": "ch_1NirD82eZvKYlo2CIvbtLWuY",
  "created": 1692942318,
  "currency": "usd",
  "destination_details": {
    "card": {
      "reference": "123456789012",
      "reference_status": "available",
      "reference_type": "acquirer_reference_number",
      "type": "refund"
    },
    "type": "card"
  },
  "metadata": {},
  "payment_intent": "pi_1GszsK2eZvKYlo2CfhZyoZLp",
  "reason": null,
  "receipt_number": null,
  "source_transfer_reversal": null,
  "status": "succeeded",
  "transfer_reversal": null
}
```

+++

>[!TAB 余额交易记录]

在[!DNL Stripe]中，**余额交易记录**&#x200B;表示您的[!DNL Stripe]帐户之间的资金流动。 有关特定余额交易属性的详细信息，请阅读余额交易的[[!DNL Stripe] API指南](https://docs.stripe.com/api/balance_transactions)。

+++选择以查看Stripe余额事务处理对象

```json
{
  "id": "txn_1MiN3gLkdIwHu7ixxapQrznl",
  "object": "balance_transaction",
  "amount": -400,
  "available_on": 1678043844,
  "created": 1678043844,
  "currency": "usd",
  "description": null,
  "exchange_rate": null,
  "fee": 0,
  "fee_details": [],
  "net": -400,
  "reporting_category": "transfer",
  "source": "tr_1MiN3gLkdIwHu7ixNCZvFdgA",
  "status": "available",
  "type": "transfer"
}
```

+++

>[!TAB 客户]

在[!DNL Stripe]中，**客户**&#x200B;代表您公司的给定客户。 有关特定客户属性的信息，请阅读有关客户的[[!DNL Stripe] API指南](https://docs.stripe.com/api/customers)，了解有关特定客户属性的更多信息。

+++选择以查看Stripe客户对象

```json
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

+++

>[!TAB 价格]

在[!DNL Stripe]中，**价格**&#x200B;表示产品循环购买和一次性购买的单位成本、货币和可选帐单周期。 有关特定价格属性的更多信息，请阅读价格[[!DNL Stripe] 的](https://docs.stripe.com/api/prices)API指南。

+++选择以查看Stripe价格对象

```json
{
  "id": "price_1MoBy5LkdIwHu7ixZhnattbh",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1679431181,
  "currency": "usd",
  "custom_unit_amount": null,
  "livemode": false,
  "lookup_key": null,
  "metadata": {},
  "nickname": null,
  "product": "prod_NZKdYqrwEYx6iK",
  "recurring": {
    "aggregate_usage": null,
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": null,
    "usage_type": "licensed"
  },
  "tax_behavior": "unspecified",
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "recurring",
  "unit_amount": 1000,
  "unit_amount_decimal": "1000"
}
```

+++

>[!ENDTABS]


### IP地址允许列表

在使用源连接器之前，必须将IP地址列表添加到允许列表中。 未能将特定于区域的IP地址添加到允许列表中，可能会导致使用源时出现错误或性能不佳。 有关详细信息，请参阅[IP地址允许列表](../../ip-address-allow-list.md)页。

### 在Experience Platform上配置权限

若要将您的&#x200B;**[!UICONTROL 帐户连接到Experience Platform，您必须同时为您的帐户启用]**&#x200B;查看源&#x200B;**[!UICONTROL 和]**&#x200B;管理源[!DNL Stripe]权限。 请联系您的产品管理员以获取必要的权限。 有关详细信息，请阅读[访问控制UI指南](../../../access-control/ui/overview.md)。

## 后续步骤

完成先决条件设置后，您可以继续连接并将[!DNL Stripe]数据摄取到Experience Platform。 请阅读以下指南，了解如何使用API或用户界面将[!DNL Stripe]付款数据摄取到Experience Platform：

* [使用流服务API将付款数据从您的Stripe帐户摄取到Experience Platform](../../tutorials/api/create/payments/stripe.md)。
* [使用用户界面](../../tutorials/ui/create/payments/stripe.md)将付款数据从Stripe帐户摄取到Experience Platform。
