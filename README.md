[![Build status](https://ci.appveyor.com/api/projects/status/80ylybuqawhvbr14?svg=true)](https://ci.appveyor.com/project/cmendible/azurebus)

AzureBus
===================

Inspired by the simple [EasyNetQ](http://easynetq.com/ "EasyNetQ") API, this library helps you get started with Microsoft Azure Service Bus or [Service Bus 1.1 for Windows Server](http://msdn.microsoft.com/en-us/library/windowsazure/dn282144.aspx) pub/sub and queues!

<pre><code>using AzureBus;

// Create a bus instance
IBus bus = AzureCloud.CreateBus();

// Publish a sample message.
bus.Publish(new SampleMessage("message value"));

// Sample consumer class
public class Consumer : IConsume&lt;SampleMessage>
{
    public void Consume(SampleMessage message)
    {
        Console.WriteLine(string.Format("Message received: Value = {0}", message.Value));
    }
}

// Subscribe to messages using consumers in an assembly.
var autoSubscriber = new AutoSubscriber(bus, "subscriptionId");
autoSubscriber.Subscribe(Assembly.GetExecutingAssembly());
</code></pre>

Queues are also supported:

<pre><code>// Create a Queue instance
IQueue queue = AzureCloud.CreateQueue();

// Subscribe to queue for messages of type SampleMessage
queue.Subscribe&lt;SampleMessage>((m) => Console.WriteLine(m.Value));

// Send message.
queue.Send(new SampleMessage("message value"));
</pre></code>

AzureBus is available as nuget package.

<pre><code>To install AzureBus, run the following command in the Package Manager Console

PM> Install-Package AzureBus</code></pre>
