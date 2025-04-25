# How to Upgrade a Data Disk using a Snapshot

## Step 1: Access Disk Settings

1. Navigate to the **Settings** section and select **Disks**.
   
   ![image](./img/SS1.png)

2. Click on the disk name to view detailed information.

   ![image](./img/SS2.png)

3. Note the following details:
   - Storage type: Premium SSD v2
   - Redundancy option: LRS
   - Size: 16364GB
   - Logical sector size: 4096 (bytes)

4. Click on **Create snapshot**.

   ![image](img/SS3.png)

## Step 2: Create a Snapshot

1. In the snapshot creation page, fill in the required fields:
   - **Name**: Provide a name for the snapshot.
   - **Snapshot type**: Keep it as "**Incremental**".
2. Click on **Review + Create**.

   ![image](img/SS4.png)

## Step 3: Create a Disk from the Snapshot and Attach the Disk

### Create a New Disk

1. Return to the **Settings/Disks** page.
2. Click on **Create and attach a new disk**.

   ![image](img/SS5.png)

3. A new disk item will appear in the view.
4. Select the desired **Storage type**. To upgrade the old disk, select **Ultra Disk**.

   ![image](img/SS6.png)
   ![image](img/SS7.png)

5. Fill in the required fields to create the new data disk:
   - **Name**: Provide a name for the new disk.
   - **Source type**: Select **Snapshot** from the dropdown.
   - **Size**: Adjust if necessary.
   - Click on **Review + Create**.

   ![image](img/SS7a.png)

### Change Disk Size (if needed)

1. Click on **Change size**.

   ![image](img/SS8.png)

2. Select the desired **Storage type** (e.g., Ultra Disk).
3. Update or keep the disk size.

4. Input **Disk IOPS** and **Disk throughput** based on the maximum values available for your (old) disk type - see above the provisioned values.

   ![image](img/SS8a.png)

5. Confirm the values are correct in the **Size** section and click **OK**.

> **Note:** [Ultra Disks](https://learn.microsoft.com/en-us/azure/virtual-machines/disks-enable-ultra-ssd?tabs=azure-portal#ga-scope-and-limitations) support a 4k physical sector size by default but also supports a 512E sector size. Most applications are compatible with 4k sector sizes, but some require 512-byte sector sizes. Oracle Database, for example, requires release 12.2 or later in order to support 4k native disks. For older versions of Oracle DB, 512-byte sector size is required.

   ![image](img/SS9a.png)

## Step 4: Verify and Attach the New Disk

1. Check that the new disk item reflects the updated values regarding storage type, size, IOPS, and throughput.

2. Click **Apply** to attach the new disk.

   ![image](img/SS10.png)

## Step 5: Detach the Old Disk

> **Note:** Before detaching the old disk, ensure the background copy process of the new disk is complete to avoid [performance impacts](https://learn.microsoft.com/en-us/azure/virtual-machines/scripts/create-managed-disk-from-snapshot#performance-impact---background-copy-process) dute to latency. 
* You can use the *CompletionPercent* property to check the status of the background copy for Ultra Disks and Premium SSD v2 disks.

   ![image](img/SS11.png)

1. Wait until the background copy is 100% completed.

   ![image](img/SS11a.png)

### Detach the Old Disk

1. Click the **detach** icon for the old disk.

   ![image](img/SS12.png)

2. Click **Apply** to confirm the detachment.

   ![image](img/SS13.png)

