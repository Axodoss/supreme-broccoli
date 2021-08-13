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

## Queues
__Task__ - _text_ 
```json
{
  "worker": "dll file",
  "id": 32,
  "type": "blah",
  "content": {
  }
}
```
__Status__ - _text_ 
```json
{
}
```

## Client-Work Interface
```c
struct FileSystem
{
    // load/save files
};

struct MessageSystem
{
    // messages
};

struct Task
{
    int id;
    char type[32];
    char content[8192]; // image content?
};

struct Context
{
	FileSystem fileSystem;
    MessageSystem messageSystem;

    // GetWorkerId
};

bool ClientInit(Context*);     // returns true on success
bool ClientUpdate(Context*);   // returns true if should keep updating
void ClientShutdown(Context*);

bool WorkerInit(Context*);     // returns true on success
void WorkerDoTask(Context*, Task*);
void WorkerShutdown(Context*);

// message serializer/deserializer
```