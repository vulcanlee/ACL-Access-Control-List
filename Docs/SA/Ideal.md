# 系統需求說明

這個專案將會針對一般企業開發系統中，必定要開發出來的一組功能，那就是權控機制，這裡需要能夠提供一個權限控制清單，讓應用程式可以做到相關控管目的，這將做到底下事情
* 使用者通過身分認證之後，將會取得可以使用存取清單 Access Control List ACL
* 這個 ACL 內將會有這名使用者會看到的功能表項目，這也包含子功能表資訊，這些功能表項目將會用於顯示在應用程式上，提供使用者切換到不同作業來進行各項操作
* 該 ACL 內也會包含每個作業內可以授權的功能，例如：新增、修改、查詢、刪除、列印、匯出、上傳等等各種功能，這些功能將會由管理者依這需要自行擴充與建立

底下將會是詳細列出各主體 Entity 需求與和其他主體之間的關係
* 一個使用者 User 將會代表一個可以登入到系統或者通過身分驗證的資料，這裡面將會包含使用者的基本資訊，當然，要符合現今資安需求來設計這個使用者主體，加入更多欄位以便進行資訊安全控管，例如，停用帳號等欄位，越完整與詳細越好。
* 使用者 User 可以加入到不同的使用者群組 UserGroup ，一個 UserGroup 將會代表一群使用者，若系統中想要進行授權或者設定的時機，可以指定一個 UserGroup 來做到一次指派大量使用者的目的
* 一個組織單元 Organization Unit , OU ，將會代表企業中的每個單位，一個 OU 將會一個父 OU，而一個 OU 可以擁有多個子 OU，可以用於表示出企業中不同單位間的關係
* OU 可以與 User 或者與 UserGroup 綁定在一起，如此，便可以知道每個 OU 內有那些使用者存在
* 一個功能集合 MenuSet 將會代表可以顯示在螢幕上的功能表關係結果
* 一個 MenuSet 將可以擁有多個子功能表 SubMenu
* 每個 SubMenu 可以擁有多個功能項目 MenuItem，也就是對應實際作業操作畫面
* 一個 MenuItem 可以設定多個操作權限 Operation Permission，這些操作權限將不是固定不變，而是可以動態的擴充，例如對於某個作業操作的 MenuItem 可以授予使用僅能夠做到查詢操作，並不能夠新增或修改和刪除，而對於另外一個 MenuItem 可以使用者將無法刪除紀錄
* 每個 MenuItem 將會有個作業代碼 Operation Code，用於綁定到某個作業操作畫面
* 對於一個 MenuItem 內指定的 Operation Permission，將會由該作業操作畫面的程式碼來時做出來，該程式依據當前的 Operation Permission 來決定是否顯示或者停用沒有授權的功能，確保僅有合法授權的使用者，可以進行符合其授權身分的操作
* 一個角色集合 RoleSet 可以包含一個或者多的 MenuSet，也就是說， RoleSet 可以用於組合出多個 MenuSet 所創建出來的新應用程式權限控管內容。
* 每個 OU 將會綁定到一個 RoleSet ，如此，一旦使用者通過身分驗證之後，就可以透過該使用者屬於那些 OU，而這些 OU 又包含了那些 RoleSet ，進而推算出該使用者將可以看到那些功能表與功能項目清單，並且可以知道每個作業可以使用那些權限

# 系統訊息

你是一位專業與有很豐富經驗的系統分析與設計師

# 分析論述

## 提問

請分析上述需求，看看是否有哪些地方設計不完善，列出這些問題並且給予更好的建議

## 回答

這個專案的設計已經相當完整，涵蓋了權限控制系統的主要元素，包括使用者、使用者群組、組織單元、功能集合、子功能表、功能項目、操作權限、作業代碼、角色集合等。然而，以下是一些可能需要進一步考慮的地方：  
   
1. 审核机制：在權限控制系統中，尤其是涉及敏感操作（如刪除、修改等）時，可能需要一個審核機制。例如，當一個使用者希望刪除一個重要資料時，這個操作可能需要由一個或多個具有更高權限的使用者來審核並批准。  
   
2. 權限繼承：在描述OU和User或UserGroup的關係時，可能需要考慮權限繼承的問題。例如，如果一個UserGroup有某個權限，那麼該UserGroup中的所有User是否也應該具有相同的權限？如果一個OU有某個權限，那麼該OU的子OU是否也應該具有相同的權限？  
   
3. 權限分離：在設計權限控制系統時，可能需要考慮權限分離的原則，以防止權限過度集中。例如，一個使用者可能不應該同時具有創建和審核同一項目的權限。  
   
4. 權限回收：當一個使用者的權限被撤銷或修改時，可能需要一個機制來確保這些變更能夠立即生效，並且不會影響已經啟動的操作。  
   
5. 異常行為檢測：權限控制系統可能需要一個機制來檢測和報告異常行為，例如，一個使用者在短時間內嘗試多次登入，或者一個使用者嘗試訪問他們通常不訪問的功能。  
   
6. 權限分配的靈活性：在設計權限控制系統時，可能需要考慮如何提供足夠的靈活性，以便能夠根據不同的業務需求來分配權限。例如，一個使用者可能需要在特定的時間段或在完成特定的任務後才能獲得某個權限。  
   
7. 記錄和審計：權限控制系統可能需要提供足夠的記錄和審計功能，以便能夠追蹤和檢查所有的權限變更和使用情況。  
   
以上是一些可能需要考慮的地方，具體的設計可能需要根據實際的業務需求和安全需求來進行調整。

## 提問

重新整理出一份完整且正式的需求分析規格文件

## 回答

# 權限控制系統需求分析規格文件  
   
## 1. 系統概述  
   
本系統將針對一般企業開發系統中，必定要開發出來的一組功能，即權控機制。該系統將提供一個權限控制清單，讓應用程式可以做到相關控管目的。  
   
## 2. 功能需求  
   
### 2.1 使用者認證  
   
使用者通過身分認證之後，將會取得可以使用存取清單 Access List ACL。  
   
### 2.2 功能表項目  
   
ACL 內將會有這名使用者會看到的功能表項目，這也包含子功能表資訊，這些功能表項目將會用於顯示在應用程式上，提供使用者切換到不同作業來進行各項操作。  
   
### 2.3 授權功能  
   
ACL 內也會包含每個作業內可以授權的功能，例如：新增、修改、查詢、刪除、列印、匯出、上傳等等各種功能，這些功能將會由管理者依這需要自行擴充與建立。  
   
## 3. 主體需求  
   
### 3.1 使用者 User  
   
一個使用者 User 將會代表一個可以登入到系統或者通過身分驗證的資料，這裡面將會包含使用者的基本資訊，包括但不限於姓名、電郵、聯絡方式等。此外，為符合現今資安需求來設計這個使用者主體，將加入更多欄位以便進行資訊安全控管，例如，停用帳號等欄位。  
   
### 3.2 使用者群組 UserGroup  
   
使用者 User 可以加入到不同的使用者群組 UserGroup ，一個 UserGroup 將會代表一群使用者，若系統中想要進行授權或者設定的時機，可以指定一個 UserGroup 來做到一次指派大量使用者的目的。  
   
### 3.3 組織單元 Organization Unit (OU)  
   
一個組織單元 Organization Unit , OU ，將會代表企業中的每個單位，一個 OU 將會一個父 OU，而一個 OU 可以擁有多個子 OU，可以用於表示出企業中不同單位間的關係。  
   
### 3.4 功能集合 MenuSet  
   
一個功能集合 MenuSet 將會代表可以顯示在螢幕上的功能表關係結果。一個 MenuSet 將可以擁有多個子功能表 SubMenu。每個 SubMenu 可以擁有多個功能項目 MenuItem，也就是對應實際作業操作畫面。  
   
### 3.5 操作權限 Operation Permission  
   
一個 MenuItem 可以設定多個操作權限 Operation Permission，這些操作權限將不是固定不變，而是可以動態的擴充。  
   
### 3.6 作業代碼 Operation Code  
   
每個 MenuItem 將會有個作業代碼 Operation Code，用於綁定到某個作業操作畫面。  
   
### 3.7 角色集合 RoleSet  
   
一個角色集合 RoleSet 可以包含一個或者多的 MenuSet，也就是說， RoleSet 可以用於組合出多個 MenuSet 所創建出來的新應用程式權限控管內容。  
   
## 4. 主體間關係  
   
### 4.1 OU 與 User 或 UserGroup 關係  
   
OU 可以與 User 或者與 UserGroup 綁定在一起，如此，便可以知道每個 OU 內有那些使用者存在。  
   
### 4.2 MenuItem 與 Operation Permission 關係  
   
對於一個 MenuItem 內指定的 Operation Permission，將會由該作業操作畫面的程式碼來時做出來，該程式依據當前的 Operation Permission 來決定是否顯示或者停用沒有授權的功能。  
   
### 4.3 OU 與 RoleSet 關係  
   
每個 OU 將會綁定到一個 RoleSet ，如此，一旦使用者通過身分驗證之後，就可以透過該使用者屬於那些 OU，而這些 OU 又包含了那些 RoleSet ，進而推算出該使用者將可以看到那些功能表與功能項目清單，並且可以知道每個作業可以使用那些權限。  
   
## 5. 異常處理  
   
系統將考慮異常情況的處理，例如，如果一個使用者被分配到不存在的功能項目或操作權限，系統將進行適當的錯誤處理。  
   
## 6. 审計和日誌  
   
系統將提供對於權限變更的審計和日誌功能，以確保系統的安全性和可追溯性。  
   
## 7. 數據保護  
   
系統將考慮到數據保護問題，例如，使用者的密碼將以安全的方式存儲，並且對於權限變更的資訊將進行適當的保護。  
   
## 8. 權限繼承和動態變更  
   
系統將明確規定權限繼承的規則，並且支援權限的動態變更。如果一個使用者的權限在其登入系統後被變更，那麼這個變更將在適當的時機生效。

## 提問

使用 Entity Framework Code 的 Code First 設計方法，建立出所需要的 Entity Model

## 回答

以下是使用Entity Framework Code First設計方法的一個基本示例，根據您的需求，我們需要建立User、UserGroup、OrganizationUnit (OU)、MenuSet、SubMenu、MenuItem、OperationPermission和RoleSet等實體模型：  
   
```csharp  
public class User  
{  
    public int Id { get; set; }  
    public string Name { get; set; }  
    public string Email { get; set; }  
    public bool IsDisabled { get; set; }  
  
    public virtual ICollection<UserGroup> UserGroups { get; set; }  
}  
   
public class UserGroup  
{  
    public int Id { get; set; }  
    public string Name { get; set; }  
  
    public virtual ICollection<User> Users { get; set; }  
}  
   
public class OrganizationUnit  
{  
    public int Id { get; set; }  
    public string Name { get; set; }  
  
    public int? ParentId { get; set; }  
    public virtual OrganizationUnit Parent { get; set; }  
  
    public virtual ICollection<OrganizationUnit> Children { get; set; }  
    public virtual ICollection<User> Users { get; set; }  
    public virtual ICollection<UserGroup> UserGroups { get; set; }  
}  
   
public class MenuSet  
{  
    public int Id { get; set; }  
    public string Name { get; set; }  
  
    public virtual ICollection<SubMenu> SubMenus { get; set; }  
}  
   
public class SubMenu  
{  
    public int Id { get; set; }  
    public string Name { get; set; }  
  
    public int MenuSetId { get; set; }  
    public virtual MenuSet MenuSet { get; set; }  
  
    public virtual ICollection<MenuItem> MenuItems { get; set; }  
}  
   
public class MenuItem  
{  
    public int Id { get; set; }  
    public string Name { get; set; }  
    public string OperationCode { get; set; }  
  
    public int SubMenuId { get; set; }  
    public virtual SubMenu SubMenu { get; set; }  
  
    public virtual ICollection<OperationPermission> OperationPermissions { get; set; }  
}  
   
public class OperationPermission  
{  
    public int Id { get; set; }  
    public string Name { get; set; }  
  
    public int MenuItemId { get; set; }  
    public virtual MenuItem MenuItem { get; set; }  
}  
   
public class RoleSet  
{  
    public int Id { get; set; }  
    public string Name { get; set; }  
  
    public virtual ICollection<MenuSet> MenuSets { get; set; }  
}  
```  
   
這些模型代表了您的需求中的各種實體，並且每個實體都有一個或多個導航屬性，用於表示與其他實體的關係。請注意，這只是一個基本的示例，您可能需要根據您的實際需求進行調整。

