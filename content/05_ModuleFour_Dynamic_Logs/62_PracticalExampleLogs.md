---
title: "Adding a Dynamic Log to our Application"
chapter: true
weight: 3
---

# Adding a Dynamic Log to our Application

Note that our application's output stream (`stdout`) is currently empty - it does not emit anything. However - our Lightrun agent is alive and well, indicating the application is indeed running.
   ![Empty Output](/images/05_Dynamic_Logs/empty-stdout.png)

Our application goes through a large range of numbers, and each time it encounters a prime, it increments a counter aptly named `cnt`. A good way to follow the process of the application is to print out the value of `cnt` every time it is incremented!

Let's add a Lightrun log - right click on line 73 (right next to the `cnt++`) and add the following log:

```
We have counted {cnt} primes so far
```
Note that you need to set the output to both `plugin` and `stdout`:

   ![Add Log](/images/05_Dynamic_Logs/add-log.png)

Inside `{expression}` you can put any Java expression you want, and it will be evaluated at runtime. In this specific case, it will enable us to see the amount of prime numbers counted at any given point of the application, since it's a loop:

```java
public static void main(String[] args) throws InterruptedException {
		for (int i = 2; i < Math.pow(10, 9); ++i) {
			if (isPrime(i)) {
				cnt++; // <-- Place a Lightrun log here
			}
			Thread.sleep(1);
		}
		System.out.println("Total number of primes: " + cnt);
	}
}
```

Click create, and watch the logs stream right into the IDE inside the "Lightrun Console" at the bottom:

   ![IDE Console Logs](/images/05_Dynamic_Logs/ide-console.png)

In addition, if you edit the action by right clicking on the action on the sidebar and then clicking `edit`, you'll be able to stream the logs to the `stdout` of the application itself!
Once the window opens, add `stdout` as a target:

   ![Edit Action](/images/05_Dynamic_Logs/edit-action.png)

And then you'll be able to see the logs streaming into the stdout of the application as well:

   ![Logs Streaming into IDE](/images/05_Dynamic_Logs/logs-streamin.png)

In addition, you might note the following message appearing in the output:

```
This action is temporarily paused by quota enforcement due to frequency of action invocation
```

This is [our sandbox in action](https://lightrun.com/security/) - making sure that the very quick loop that checks the primality (happens hundreds of times each second) does not cause the logs to be emitted to frequently, thus jeopardizing the integrity of the application.

Now that you've seen Lightrun in Action, let's clean up the workspace.