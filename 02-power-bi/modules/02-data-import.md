# Module 2: Data Import & Connectivity

## Data Source အမျိုးအစားများ

Power BI သည် data source အမျိုးမျိုးမှ data များကိုချိတ်ဆက်နိုင်ပြီး source အမျိုးအစားပေါင်း 150+ ကျော်ကို built-in connectors များဖြင့်ပံ့ပိုးထားပါသည်။

### File Sources

| Source | Description | File Extension |
|--------|-------------|----------------|
| Excel | Spreadsheet data | .xlsx, .xls, .xlsm |
| CSV/Text | Delimited text files | .csv, .txt, .tsv |
| JSON | JavaScript Object Notation | .json |
| XML | Extensible Markup Language | .xml |
| PDF | Extract tables from PDF | .pdf |
| Folder | Combine multiple files in folder | — |
| SharePoint Folder | Online file repository | — |

### Database Sources

| Source | Connector Type |
|--------|---------------|
| SQL Server | Native, DirectQuery |
| PostgreSQL | Native, ODBC |
| MySQL | Native, ODBC |
| Oracle | Native |
| Snowflake | Native, DirectQuery |
| Azure SQL Database | Native |
| Azure Synapse | Native |
| Google BigQuery | Native |

### Cloud & Online Services

- SharePoint Online, Dynamics 365, Salesforce, Google Analytics, Adobe Analytics, Facebook, GitHub, Zendesk, MailChimp, Marketo...

### Import Steps

**From Excel:** Home → Get Data → Excel → Select File → Navigator → Choose Tables/Sheets → Load

**From SQL Server:** Get Data → SQL Server → Enter Server/Database → Select Import/DirectQuery → Choose Tables → Load

### Connection Settings

| Setting | Description |
|---------|-------------|
| Import | Data ကို Power BI ထဲသို့ copy လုပ် (in-memory cache) |
| DirectQuery | Data ကို source မှတိုက်ရိုက်ယူ (no cache) |
| Live Connection | Existing dataset/semantic model ကိုတိုက်ရိုက်သုံး |



## Data Connectivity Best Practices

1. **Credentials ကိုသေချာစီမံပါ** — Store credentials in Gateway (on-prem) or use service principal (cloud)
2. **Query Folding ကိုသုံးပါ** — Source-level filtering လုပ်ပါ (SQL WHERE clause)
3. **Parameters သုံးပါ** — Server/database names ကို parameter ဖြင့်သတ်မှတ်ပါ (easy to change)
4. **Data Source Settings ကို Document လုပ်ပါ** — Gateway connections, credentials, paths
5. **Performance Test လုပ်ပါ** — Large dataset များအတွက် import time ကိုစစ်ဆေးပါ

### Data Source Settings Management

Power BI Desktop တွင် Home → Transform Data → Data Source Settings → Change Source ဖြင့် connection settings များကိုပြောင်းလဲနိုင်ပါသည်။

### Privacy Levels

| Level | Description |
|-------|-------------|
| Organizational | Company-internal data sources |
| None | No privacy restrictions |
| Private | Restricted data (cannot be shared) |
| Public | Open data sources |

### Gateway Installation Requirements

- Windows Server 2016+ or Windows 10/11 Pro
- .NET Framework 4.7.2+
- Minimum 4GB RAM, 2 CPU cores
- Outbound HTTPS (port 443) to Azure
- Service account with appropriate permissions


## Advanced Data Connectivity

### Connecting to SQL Server in Detail

SQL Server ကိုချိတ်ဆက်ရာတွင် အောက်ပါအချက်များကိုထည့်သွင်းစဉ်းစားရန် လိုအပ်ပါသည်-

**Server Name formats:**
- Local: localhost, . , (local)
- Named instance: SERVERNAME\\INSTANCENAME
- IP Address: 192.168.1.100, 10.0.0.5
- Azure: servername.database.windows.net

**Database Selection:**
- Database name အတိအကျထည့်ရန်
- Windows Auth vs SQL Auth ကိုရွေးချယ်ရန်
- Advanced options: Command timeout, SQL statement

**Connection Security:**
- Encrypt connection: သေချာစစ်ဆေးရန် (အထူးသဖြင့် cloud database)
- Trust server certificate: Development အတွက်သာ
- Firewall rules: IP whitelisting လိုအပ်နိုင်

### Importing from Excel Files

Excel files များမှ data သွင်းရာတွင်:

1. **Single Sheet:** Navigator ထဲမှ sheet ကိုရွေးပါ
2. **Multiple Sheets:** Shift/Ctrl ဖြင့်ရွေးပါ သို့မဟုတ် folder connector သုံးပါ
3. **Named Ranges:** Excel named ranges များကိုပါရွေးနိုင်
4. **PivotTables:** Raw data ကို prefer လုပ်ပါ (PivotTable ကိုတိုက်ရိုက်မသုံးရ)
5. **Multiple Files:** Folder connector သုံးပြီး folder တစ်ခုလုံးမှ data များကိုပေါင်းစပ်နိုင်

**Excel Import Tips:**
- First row as headers ကိုသေချာစစ်ပါ
- Column data types ကိုစစ်ဆေးပါ (numbers များ text ဖြစ်မနေစေရန်)
- Remove blank rows/columns များကို Power Query ဖြင့်ဖယ်ရှားပါ
- Table format ကိုသုံးပါ (Ctrl+T) — named ranges ထက်ပိုကောင်းပါသည်

### REST API Integration

Web API များမှ data သွင်းရန်:
1. Get Data → Web → Enter API URL
2. Authentication: Anonymous, Basic, OAuth2, API Key
3. JSON/XML parsing ကို Power Query ဖြင့်လုပ်ဆောင်ပါ
4. Pagination handling အတွက် custom M code လိုအပ်နိုင်

### Data Profiling Tools

Power Query တွင် data profiling tools များပါဝင်ပါသည်:
- Column quality: % valid, % error, % empty
- Column distribution: Value frequency
- Column profile: Statistics (min, max, avg, distinct)

ဤ tools များကို View → Data Preview → Column quality, Column profile, Column distribution မှဖွင့်နိုင်ပါသည်။
## Advanced Data Connectivity

### Connecting to SQL Server in Detail

SQL Server ကိုချိတ်ဆက်ရာတွင် အောက်ပါအချက်များကိုထည့်သွင်းစဉ်းစားရန် လိုအပ်ပါသည်-

**Server Name formats:**
- Local: localhost, . , (local)
- Named instance: SERVERNAME\\INSTANCENAME
- IP Address: 192.168.1.100, 10.0.0.5
- Azure: servername.database.windows.net

**Database Selection:**
- Database name အတိအကျထည့်ရန်
- Windows Auth vs SQL Auth ကိုရွေးချယ်ရန်
- Advanced options: Command timeout, SQL statement

**Connection Security:**
- Encrypt connection: သေချာစစ်ဆေးရန် (အထူးသဖြင့် cloud database)
- Trust server certificate: Development အတွက်သာ
- Firewall rules: IP whitelisting လိုအပ်နိုင်

### Importing from Excel Files

Excel files များမှ data သွင်းရာတွင်:

1. **Single Sheet:** Navigator ထဲမှ sheet ကိုရွေးပါ
2. **Multiple Sheets:** Shift/Ctrl ဖြင့်ရွေးပါ သို့မဟုတ် folder connector သုံးပါ
3. **Named Ranges:** Excel named ranges များကိုပါရွေးနိုင်
4. **PivotTables:** Raw data ကို prefer လုပ်ပါ (PivotTable ကိုတိုက်ရိုက်မသုံးရ)
5. **Multiple Files:** Folder connector သုံးပြီး folder တစ်ခုလုံးမှ data များကိုပေါင်းစပ်နိုင်

**Excel Import Tips:**
- First row as headers ကိုသေချာစစ်ပါ
- Column data types ကိုစစ်ဆေးပါ (numbers များ text ဖြစ်မနေစေရန်)
- Remove blank rows/columns များကို Power Query ဖြင့်ဖယ်ရှားပါ
- Table format ကိုသုံးပါ (Ctrl+T) — named ranges ထက်ပိုကောင်းပါသည်

### REST API Integration

Web API များမှ data သွင်းရန်:
1. Get Data → Web → Enter API URL
2. Authentication: Anonymous, Basic, OAuth2, API Key
3. JSON/XML parsing ကို Power Query ဖြင့်လုပ်ဆောင်ပါ
4. Pagination handling အတွက် custom M code လိုအပ်နိုင်

### Data Profiling Tools

Power Query တွင် data profiling tools များပါဝင်ပါသည်:
- Column quality: % valid, % error, % empty
- Column distribution: Value frequency
- Column profile: Statistics (min, max, avg, distinct)

ဤ tools များကို View → Data Preview → Column quality, Column profile, Column distribution မှဖွင့်နိုင်ပါသည်။
## Advanced Data Connectivity

### Connecting to SQL Server in Detail

SQL Server ကိုချိတ်ဆက်ရာတွင် အောက်ပါအချက်များကိုထည့်သွင်းစဉ်းစားရန် လိုအပ်ပါသည်-

**Server Name formats:**
- Local: localhost, . , (local)
- Named instance: SERVERNAME\\INSTANCENAME
- IP Address: 192.168.1.100, 10.0.0.5
- Azure: servername.database.windows.net

**Database Selection:**
- Database name အတိအကျထည့်ရန်
- Windows Auth vs SQL Auth ကိုရွေးချယ်ရန်
- Advanced options: Command timeout, SQL statement

**Connection Security:**
- Encrypt connection: သေချာစစ်ဆေးရန် (အထူးသဖြင့် cloud database)
- Trust server certificate: Development အတွက်သာ
- Firewall rules: IP whitelisting လိုအပ်နိုင်

### Importing from Excel Files

Excel files များမှ data သွင်းရာတွင်:

1. **Single Sheet:** Navigator ထဲမှ sheet ကိုရွေးပါ
2. **Multiple Sheets:** Shift/Ctrl ဖြင့်ရွေးပါ သို့မဟုတ် folder connector သုံးပါ
3. **Named Ranges:** Excel named ranges များကိုပါရွေးနိုင်
4. **PivotTables:** Raw data ကို prefer လုပ်ပါ (PivotTable ကိုတိုက်ရိုက်မသုံးရ)
5. **Multiple Files:** Folder connector သုံးပြီး folder တစ်ခုလုံးမှ data များကိုပေါင်းစပ်နိုင်

**Excel Import Tips:**
- First row as headers ကိုသေချာစစ်ပါ
- Column data types ကိုစစ်ဆေးပါ (numbers များ text ဖြစ်မနေစေရန်)
- Remove blank rows/columns များကို Power Query ဖြင့်ဖယ်ရှားပါ
- Table format ကိုသုံးပါ (Ctrl+T) — named ranges ထက်ပိုကောင်းပါသည်

### REST API Integration

Web API များမှ data သွင်းရန်:
1. Get Data → Web → Enter API URL
2. Authentication: Anonymous, Basic, OAuth2, API Key
3. JSON/XML parsing ကို Power Query ဖြင့်လုပ်ဆောင်ပါ
4. Pagination handling အတွက် custom M code လိုအပ်နိုင်

### Data Profiling Tools

Power Query တွင် data profiling tools များပါဝင်ပါသည်:
- Column quality: % valid, % error, % empty
- Column distribution: Value frequency
- Column profile: Statistics (min, max, avg, distinct)

ဤ tools များကို View → Data Preview → Column quality, Column profile, Column distribution မှဖွင့်နိုင်ပါသည်။
