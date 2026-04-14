# Transactional Writes & Auto Backup

**What are the best practices in Android 14 to prevent data loss due to power failure?**

In Android 14 (API level 34), the core strategy to prevent data loss due to power failure revolves around leveraging **Auto Backup**, adhering to **proper storage directory specifications**, using **transactional writes** for critical data, and properly managing **database synchronization (Checkpoints)**.

Here is the best practice solution for Android 14:

#### 1. Choosing the Data Storage Location

The storage location directly determines the data lifecycle and backup behavior.

* **Preferred: Internal Storage**: Use `Context.getFilesDir()` or `Context.getDataDir()`. This part of the storage is private to the app, its stability is guaranteed by the system, and it forms the foundation for the Auto Backup feature.
* **Avoid Cache Directories**: Never store important data in `getCacheDir()` or `getExternalCacheDir()`. If the system detects a restart after a power failure or if storage space is low, these directories may be cleared by the system at any time.

#### 2. Ensuring Atomicity for Database Writes

For SQLite databases (often used with Room), Android 14 introduces a more powerful compiler supporting **vectorized exceptions**, but data integrity still relies on developer coding habits.

* **Ensure the Use of Transactions**: In Room, for any `insert`, `update`, or `delete` methods that contain multiple write operations, be sure to use the `@Transaction` annotation. This ensures that the entire series of operations either succeeds or fails completely (atomicity), avoiding the "half-finished" data state caused by a power interruption mid-write.
*   **Configure WAL Mode and Manual Checkpointing**: To maximize the prevention of data loss due to power failure, you can refer to the following practices:

    **1）Set Journal Mode**: When building the Room database, you can set `setJournalMode(RoomDatabase.JournalMode.TRUNCATE)`. This sets the journal mode to rollback mode, sacrificing some concurrency performance in exchange for extremely high data security, ensuring that any uncommitted transactions will not persist after a crash.

    <figure><img src="../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

    **2）Manually Trigger a Checkpoint**: If you choose WAL (Write-Ahead Logging) mode for performance, after performing add, delete, or modify operations on critical data, you can force the changes in the WAL file to be synchronized to the main database file. Executing `execSQL("PRAGMA wal_checkpoint(FULL);")` or closing the database connection can trigger synchronization, ensuring data is physically written to disk.

#### 3. Synchronization Strategy for File Writes

For scenarios involving direct file operations, merely calling `write()` is insufficient, as data may still reside in the operating system's page cache.

* **Force Flush to Disk**: After completing a write of critical data, you should call the `sync()` method of the `FileDescriptor` (via `FileOutputStream.getFD().sync()`). This forces the system to immediately write the file cache to the storage medium and is the most direct protective measure against data loss due to power failure.

#### Summary

To prevent data loss in Android 14, adopt a combined strategy of "**cloud backup + local atomic writes + synchronous persistence to disk**":

1. **Cloud**: Leverage **Auto Backup** for disaster recovery capabilities.
2. **Library**: Use **Room transactions** and configure the **Journal Mode** to ensure database state consistency.
3. **Files**: Call **`sync()`** after writing critical files to ensure physical persistence to disk.
