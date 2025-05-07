
# Azure App Service Backup Configuration

## Introduction
Step-by-steps process to configure and validate the backup setup for an Azure App Service. The configuration ensures that backups are stored in a durable and reliable Azure Storage account and can be restored efficiently in case of a failure or disaster.

---

## Steps to Configure Backup

### 1. **Prerequisites**
- Access to the Azure Portal.
- Contributor or Owner role for the Azure Subscription.
- Existing Azure App Service WebApp.
- Permissions to create a Storage Account.  //optional if we consider to choose custom backup only.

---

### 2. **Create a Storage Account for Backup**
1. Navigate to the Azure Portal.
2. In the search bar, type `Storage Accounts` and click on the result.
3. Click **+ Create**.
4. Fill in the details:
   - **Subscription**: Select the subscription for your WebApp.
   - **Resource Group**: Use an existing one or create a new one.
   - **Storage Account Name**: Enter a unique name (e.g., `webappbackups`).
   - **Region**: Select the same region as your WebApp for optimal performance.
   - **Performance**: Standard.
   - **Redundancy**: Choose Geo-Redundant Storage (GRS) for high availability.
5. Click **Review + Create**, then **Create**.

---

### 3. **Create a Container in the Storage Account**
1. Go to the newly created Storage Account.
2. In the left menu, click **Containers** under the **Data Storage** section.
3. Click **+ Container**.
4. Provide a name (e.g., `webapp-backups`) and set the **Public Access Level** to **Private**.
5. Click **Create**.

---

### 4. **Configure Backup for the WebApp**
1. Navigate to your Azure WebApp in the Azure Portal.
2. In the left-hand menu, go to **Backups** under the **Settings** section.
3. Click **Configure Custom Backups**.
4. In the side pane:
   - **Storage Account**: Select the storage account created earlier.
   - **Container**: Choose the container created (e.g., `webapp-backups`).
5. Tick the box for **Backup/Restore over Virtual Network Integration** if your storage account uses a private endpoint.
6. Click **Save**.

---

### 5. **Set the Backup Schedule**
1. After saving the storage account configuration, click **Set Schedule**.
2. Configure the backup schedule:
   - **Repeat Every**: `1 Hour` (or adjust based on your needs).
   - **Start Time**: Choose off-peak hours (e.g., `02:00 UTC`).
   - **Time Zone**: Select **UTC** for consistency.
   - **Retention**: Set to `30 Days` (or adjust as per requirements).
   - **Keep at Least One Backup at All Times**: Tick this box.
3. Click **Save**.

---

### 6. **Trigger a Manual Backup**
1. Navigate back to the **Backups** section of your WebApp.
2. Click **Backup Now** to trigger a manual backup.
3. Monitor the progress in the **Backup Status** section.
4. Verify that the backup appears in the storage container.

---

### 7. **Validate the Restore Process**
1. In the **Backups** section, click **Restore**.
2. Select a backup from the list.
3. Configure the restore options:
   - **Choose Destination**: Current WebApp or deployment slot.
   - **Advanced Options**:
     - Tick **Restore Site Configuration** if you need to restore app settings and configurations.
4. Click **Restore** and monitor the process.

---

## Adding Screenshots in Markdown
To add screenshots, use the following syntax in your `.md` file:
```markdown
![Description of Image](path/to/image.png)
```

For example:
```markdown
![Backup Configuration Screenshot](images/backup-configuration.png)
```

Ensure you upload the screenshots to the same repository where the `.md` file is stored and adjust the path accordingly.

---

## Best Practices
- **Monitor Backups**: Regularly verify backup status to ensure they are successful.
- **Test Restore**: Periodically perform test restores to validate recovery procedures.
- **Retention Policies**: Balance retention duration with storage costs.
- **Redundancy**: Use Geo-Redundant Storage (GRS) for critical applications.

---

## Conclusion
This step-by-step guide ensures that your Azure WebApp backups are reliable and durable, providing a robust disaster recovery strategy. Test and refine this setup during the PoC to align with your organizational needs.