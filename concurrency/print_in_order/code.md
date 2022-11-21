### Code №1 (Semaphore)

    class Foo {

      Semaphore oneSema = new Semaphore(1);
      Semaphore twoSema = new Semaphore(1);
    
      public Foo() {
          oneSema.tryAcquire();
          twoSema.tryAcquire();
      }

      public void first(Runnable printFirst) throws InterruptedException {        
          // printFirst.run() outputs "first". Do not change or remove this line.
          printFirst.run();
          oneSema.release();
      }

      public void second(Runnable printSecond) throws InterruptedException {
          oneSema.acquire();
          // printSecond.run() outputs "second". Do not change or remove this line.
          printSecond.run();
          twoSema.release();        
      }

      public void third(Runnable printThird) throws InterruptedException {
          twoSema.acquire();
          // printThird.run() outputs "third". Do not change or remove this line.
          printThird.run();
      }
    }

### Code №2 (volatile int i)

    class Foo {
    
      private volatile int i = 1;

      public Foo() {
        
      }

      public void first(Runnable printFirst) throws InterruptedException {
        while (i != 1);
        
        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        
        i = 2;
      }

      public void second(Runnable printSecond) throws InterruptedException {
        while (i != 2);
        
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        
        i = 3;
      }

      public void third(Runnable printThird) throws InterruptedException {
        while (i != 3);
        
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
        
        i = 1;
      }
    }

### Code №3 (AtomicInteger)
    class Foo {
    
      private final AtomicInteger sec;

      public Foo() {
        this.sec = new AtomicInteger(1);
      }

      public void first(Runnable printFirst) throws InterruptedException {
        while (sec.get() != 1) {
            // self-checking……
        }
        printFirst.run();
        sec.getAndIncrement();
      }

      public void second(Runnable printSecond) throws InterruptedException {
        while (sec.get() != 2) {
            // self-checking……
        }
        printSecond.run();
        sec.getAndIncrement();
      }

      public void third(Runnable printThird) throws InterruptedException {
        while (sec.get() != 3) {
             // self-checking……
        }
        printThird.run();
      }
    }

### Code №4 (CountDownLatch)

    class Foo {
      private CountDownLatch first = new CountDownLatch(1);
      private CountDownLatch second = new CountDownLatch(1);
    
      public Foo() {}

      public void first(Runnable printFirst) throws InterruptedException {
        
        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        first.countDown();
      }

      public void second(Runnable printSecond) throws InterruptedException {
        first.await();
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        second.countDown();
      }

      public void third(Runnable printThird) throws InterruptedException {
        first.await();
        second.await();
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
      }
    }

### Code №5 (synchronized)

    class Foo {
      private static enum PrintState {
        ZERO, DID1, DID2
      }
      private PrintState printState = PrintState.ZERO;
    
      public Foo() {}

      public synchronized void first(Runnable printFirst) throws InterruptedException {
        while(printState != PrintState.ZERO) wait();
        // printFirst.run() outputs "first". Do not change or remove this line.
        printFirst.run();
        printState = PrintState.DID1;
        notifyAll();
      }

      public synchronized void second(Runnable printSecond) throws InterruptedException {
        while(printState != PrintState.DID1) wait();
        // printSecond.run() outputs "second". Do not change or remove this line.
        printSecond.run();
        printState = PrintState.DID2;
        notifyAll();
      }

      public synchronized void third(Runnable printThird) throws InterruptedException {
        while(printState != PrintState.DID2) wait();
        // printThird.run() outputs "third". Do not change or remove this line.
        printThird.run();
        printState = PrintState.ZERO;
        notifyAll();
      }
    }
