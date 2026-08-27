# DNS Configuration for vWAF

After creating an application on vWAF, traffic only actually passes through the WAF once **your service domain has been pointed to the vWAF system via DNS**. Until DNS is configured, the application still shows as _Active_ in the portal, but the WAF is **not protecting** your live traffic.

GreenNode supports **two methods in parallel**:

|                                    | **CNAME** _(recommended)_                                           | **A Record**                                         |
| ---------------------------------- | ------------------------------------------------------------------- | ---------------------------------------------------- |
| Record points to                   | A dedicated DNS domain issued by GreenNode                          | The vWAF public IP address                           |
| Routing changes between vWAF zones | Performed by GreenNode, **no action required from you**             | You must update your DNS yourself                    |
| Time to apply a routing change     | Fast (based on the TTL of the record GreenNode manages)             | Depends on how quickly you update DNS + your own TTL |
| Works for Root Domain (Apex)       | Only if your DNS Provider supports ALIAS / ANAME / CNAME Flattening | Works in all cases                                   |
| Works for subdomains               | Yes                                                                 | Yes                                                  |

> **Recommendation:** GreenNode recommends reviewing your current DNS configuration and moving to the **CNAME** method if your DNS Provider supports it. This method gives you greater operational flexibility and lets GreenNode steer traffic proactively while running the vWAF service.

***

### 1. CNAME method (recommended)

#### 1.1. How it works

With the CNAME method, GreenNode adds a **DNS indirection layer that GreenNode controls**:

* GreenNode issues **each customer a dedicated DNS domain** (the _vWAF routing domain_).
* You configure a **CNAME Record** for your service domain pointing to the DNS domain provided by GreenNode.
* That routing domain resolves to the vWAF zone currently serving you. When routing needs to be optimised or adjusted, GreenNode **updates DNS on the GreenNode side** to move traffic to the appropriate vWAF zone, **without requiring any DNS change on your side**.

```
           You configure this once                  Managed by GreenNode
             (one-time setup)                       (updated proactively)
                      │                                      │
                      ▼                                      ▼
www.example.com ────CNAME────▶ opnclhqr.waf.greennode.vn ────A────▶ vWAF zone (IP)
```

As a result, traffic steering between vWAF zones happens proactively on the GreenNode side, which **shortens the time needed** to apply a routing change.

#### 1.2. Finding your vWAF routing domain

The routing domain is **unique to your account** and **does not change** for the lifetime of the service (including when you add, edit, or delete applications). You only need to configure the CNAME once per service domain.

The domain has the form `<routing-code>.waf.greennode.vn`, where `<routing-code>` is an 8-character string generated automatically by GreenNode and bound to your account.

**Example:**

```
opnnqpqr.waf.greennode.vn
```

To find the routing domain issued to your account, go to **GreenNode Portal → vWAF → Applications**. It is shown in the notice box above the application list:

> To ensure all traffic is audited and protected by GreenNode WAF:
>
> * **Recommended:** Point your domain to the CNAME `<routing-code>.waf.greennode.vn`.
> * **Alternative:** If CNAME cannot be used, point your domain's DNS A record to `vwaf_public_ip`.

> **Note:** `opnnqpqr.waf.greennode.vn` above is only an illustrative example, and the routing code in the screenshot has been masked. Always use the routing domain shown in the portal for your own account. If you do not see this notice box, please contact GreenNode support.

#### 1.3. Configuration steps

1. Sign in to the DNS management console of the DNS provider hosting your service domain.
2. **Create a CNAME record** pointing to your vWAF routing domain.
3. Save and wait for DNS propagation, then verify as described in **section 4**.

**Example configuration:**

| Type  | Name / Host | Value / Target              | TTL |
| ----- | ----------- | --------------------------- | --- |
| CNAME | `@`         | `opnnqpqr.waf.greennode.vn` | 300 |
| CNAME | `api`       | `opnnqpqr.waf.greennode.vn` | 300 |

Result: both `example.com` and `api.example.com` are served through vWAF.

***

### 2. A Record method

The A Record method remains fully supported and is **unchanged** from the current behaviour. Point your service domain's A record directly to the vWAF public IP address

**Example configuration:**

| Type | Name / Host | Value         | TTL |
| ---- | ----------- | ------------- | --- |
| A    | `www`       | `103.7.174.5` | 300 |
| A    | `@`         | `103.7.174.5` | 300 |

> **Operational note:** With the A Record method, whenever GreenNode needs to move traffic to a different vWAF zone, **you must update the DNS record yourself**. This increases the time required to apply urgent routing changes.

***

### 3. Root Domain (Apex / Zone Apex)

Per the DNS standard, a **CNAME record cannot be created at the Root Domain** (for example `example.com`, with no subdomain). You can handle this in one of the following ways:

| Situation                                                                                               | How to handle it                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Your DNS Provider supports **ALIAS / ANAME / CNAME Flattening** (Cloudflare, AWS Route 53, DNSimple, …) | Create an ALIAS/ANAME/flattened CNAME record at the Root Domain pointing to `<routing-code>.waf.greennode.vn`. You keep the benefits of the CNAME method. |
| Your DNS Provider **does not support it**                                                               | Continue using an **A Record** pointing directly to the vWAF IP `103.7.174.2`, as today.                                                                  |

> **Note:** With ALIAS / CNAME Flattening, how quickly a routing change takes effect depends on how the DNS Provider implements it and the TTL it applies, and may be slower than a plain CNAME.

GreenNode supports both the CNAME and A Record methods in parallel, depending on what your DNS Provider supports and on your deployment model.

***

### 4. Verifying the configuration

**Check the CNAME record:**

```bash
dig +short CNAME example.com
# Expected result:
# opnnqpqr.waf.greennode.vn.
```

**Check the final resolved IP address:**

```bash
dig +short example.com
# Expected result: the IP address of the vWAF zone
```

**Check that traffic is flowing through vWAF:**

```bash
curl -I https://example.com
```
