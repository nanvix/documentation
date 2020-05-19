# Kernel Calls

## Memory System

- `err = pgmap(vaddr, mode)`
- `err = pgunmap(vaddr)`
- `err = pgctl(vaddr, mode)`

## Thread Management

- `tid = kthread_self()`
- `err = kthread_create(&id, start, arg)`
- `err = kthread_join(tid, &retval)`
- `err = kthread_exit(status)`

## Thread Synchronization

- `tid = kthread_sleep()`
- `err = kthread_wakeup(tid)`

## Signals

- `err = alarm(millisec)`
    
- `err = sigsend(signum, tid)`
    
- `err = sigwait(signum)`
    
- `err = sigctl(signum, ...)`
    
- `sigreturn()`
    

# Device System

- `err = inctl(intnum, ...)`
    
- `intnum = intwait()`
    
- `nread = ioread(ionum, &buf, nbytes)`
    
- `nwriten = iowrite(ionum, &buf, nbytes)`
    
- `err = iograb(ionum)`
    
- `err = iorelease(ionum)`
    
- `nread = mmioread(mmio, off, buf, nbytes)`
    
- `nwriten = mmiowrite(mmio, off, buf, nbytes)`
    
- `mmio = mmiograb(addr, size)`
    
- `err = mmiorelease(mmio)`
