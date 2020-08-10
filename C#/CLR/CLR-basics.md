## CLR
### Basics

- The Common Language Runtime (CLR) is just what its name says it is: a runtime that is usable by different and varied programming languages. The core functionality of the CLR such as memory management, assembly loading, security, exception handling and thread synchronization are available to any and all programming languages that target it - period.
- Every compiler targeting CLR is required to emit IL and full metadata into every managed module.
- Metadata is a set of data tables that describe what is defined in the module, such as types and members. In addition, metadata also has tables indicating what the managed module references, such as imported types and members.
- Metadata is always associated with the file that contains the IL code. Metadata is always embedded in the same EXE/DLL as the code, making it impossible to seperate the two.

### Uses of metadata

- All the information about the referenced types/members is contained int the file that has IL that impliments the types and members. Compilers can read metadata directly from managed modules.
- Visual studio uses metadata to help you write the code. Its IntelliSense feature parses metadata to tell us what methods, properties, events, and fields a type offers, and in the case of methods, what parameters the method expects.
- The CLR's code verification process uses metadata to ensure that code performs only 'type-safe' operations.
- Metadata allows an object's fields to be serialized into a memory blck, sent to another machine, and then deserialized, re-creating the object's state on the remote computer.
- Metadata allows garbage collectors to track the lifetime of the objects.