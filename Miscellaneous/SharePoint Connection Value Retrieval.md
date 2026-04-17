# SharePoint Value Retrieval Cheat Sheet

### <VIEWGUID>
**The unique ID for a specific view.**
1. Open the list/library and select the desired view.
2. Go to **List Settings** > Scroll to **Views** > Click the View Name.
3. In the URL, copy the string after `View=`.
4. Replace encoded characters: `%7B` → `{`, `%2D` → `-`, `%7D` → `}`.

### <LISTNAME>
**The unique ID (GUID) for the list itself.**
1. Go to **List Settings**.
2. In the URL, copy the string after `List=`.
3. Replace encoded characters: `%7B` → `{`, `%2D` → `-`, `%7D` → `}`.
*Note: If you need the display name, it is at the top of the List Settings page.*

### <LISTWEB>
**The full URL of the site containing the list.**
1. Navigate to the list.
2. Copy the URL from the browser up to the site name.
*Example: `https://sharepoint.com`*

### <LISTSUBWEB>
**The relative path of the subsite if the list is not in the root site.**
1. Check your URL for paths after `/sites/` or `/teams/`.
2. If your list is at `.../sites/Main/Finance/Lists/Expenses`, the subweb is `/Finance`.
*Note: If the list is on the main site, this value is often left blank or set to `/`.*

### <ROOTFOLDER>
**The server-relative URL path to the list/library.**
1. Go to **List Settings** > **List name, description and navigation**.
2. Look at the **Web address** field.
*Format: `/sites/SiteName/Lists/ListName` or `/sites/SiteName/LibraryName`*
