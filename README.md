# Supreme Broccoli
Workload Distribution Engine

```
                                      +--------------------------------+
                                      |        Docker Container        |
                                      |                                |
+--------------------------------+    | +----------------------------+ |    +--------------------------------+
|  Workload Distribution Engine  | => | |      Samba File Share      | | => |  Workload Distribution Engine  |
|                                | <= | +----------------------------+ | <= |                                |
| +----------------------------+ |    |                                |    | +----------------------------+ |
| | Client-Work Implementation | | => | +----------------------------+ | => | | Client-Work Implementation | |
| +----------------------------+ | <= | |     Message/Work Queue     | | <= | +----------------------------+ |
+--------------------------------+    | +----------------------------+ |    +--------------------------------+
                                      +--------------------------------+
```

## Client-Work Interface
```c

struct Task
{

};

struct Context
{
	// File System
	// Message System
};

bool ClientInit(Context*);     // returns true on success
bool ClientUpdate(Context*);   // returns true if should keep updating
void ClientShutdown(Context*);

bool WorkerInit(Context*);     // returns true on success
void WorkerDoTask(Context*, Task*);
void WorkerShutdown(Context*);

// message serializer/deserializer
```