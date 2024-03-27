# Lecture 18 <div style="text-align:right"> 22/03/2024 </div>

## API Virtualization
- Intercept and interject functionality at the APIs layer
- clients / programs use API to build logic and API calls are executed transparently by hypervisor intervention 
- eg:- give access on the cloud network

```

application
library
Drive       | Highly Coupled
GPU         | 
```

- save and restore to GPU costly

decoupling of access and device
- The API is the interface for interjection
- Hijack the call and trasport to the backend
