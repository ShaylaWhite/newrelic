# New Relic 

- Email Address: shayladwhite1@gmail.com
- Perma Link: [New Relic Application](https://onenr.io/0ERzPXVMAQr)

## Exercise Questions


### Exercise Question #1

Naming Methods for New Relic Applications
You can change the app's name in your config file, or assign an alias to the app to change how it appears in the New Relic UI
In Java, you can set up to three app names. The primary app name is first, while the second and third names are used for the more general data aggregation categories.
- Java config file
- Java environment variable
- System properties

Name your Java application: 
- Recommended: Configure `app_name` in `newrelic.yml`

- Configure app_name using JVM arguments

- Set app name using environment variables

- Automatic application naming

- Change alias via UI

#### Did you know? 
To keep things consistent and easy to navigate, New Relic recommends standardizing your application naming (for example, all apps in Staging append [Staging] or the like at the end of their names). Ideally, you want your new Java applications to be named automatically to reduce the chances of typographical errors and misnaming.
  
Source: https://docs.newrelic.com/docs/apm/agents/java-agent/configuration/name-your-java-application/

Source: https://docs.newrelic.com/docs/apm/agents/manage-apm-agents/app-naming/name-your-application/

</br>

### Exercise Question #2

Generating a Slow Transaction

I successfully connected my Java agent and ran the application. I accessed the APM data for my application, but I'm unsure if the results are being captured. 
- Can you find a “transaction trace” for the transaction in the New Relic UI? Located on New Relic UI
-  What is it telling you? No results, unsure if data is being captured via java application on my local device.
  
``` bash 
package com.example.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.redis.core.StringRedisTemplate;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @Autowired
    private StringRedisTemplate redisTemplate;

    @GetMapping("/")
    public String hello() {
        // Set a value in Redis
        redisTemplate.opsForValue().set("greeting", "Hello, Redis!");

        // Simulate a slow transaction (more than 3 seconds)
        try {
            Thread.sleep(4000); // Sleep for 4 seconds
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // Retrieve the value from Redis
        String greeting = redisTemplate.opsForValue().get("greeting");

        return "Message from Redis: " + greeting;
    }
}
```


 </BR>

### Exercise Question #3
Write a NRQL query showing your application’s throughput.  
<img width="1280" alt="image" src="https://github.com/user-attachments/assets/6b351299-421f-4330-97a3-435c8ecf4d23">




</BR>

### Exercise Question #4
Looking at the New Relic APM Summary page how would you tell if your application was performing as expected?

The green in Services and Infrastrucutre indicates that you application is in good health! 
<img width="1274" alt="image" src="https://github.com/user-attachments/assets/d79a8933-ec6a-4232-b77c-8745d828a46a">


</BR>

### Exercise Question #5
Imagine a scenario where a customer is describing how the New Relic agent doesn’t appear to be reporting data when they deploy their application.  How  would you handle this support issue? 

#### Customer:
Hi there, I've deployed our application but it seems like the New Relic agent isn’t picking up any data. Can you help?

#### Java APM Agent:
Hi! I'll do my best to assist. Let's start by checking a few things. Have you reviewed the configuration files to ensure everything is correctly set up with the New Relic agent?

#### Customer:
Yes, I double-checked the configuration files and restarted the application server, but still no luck.

#### Java APM Agent:
Got it. In this case, I recommend we take a closer look at the agent logs to see if there are any specific errors or warnings that might give us more insight. Also, have you visited New Relic's best practices for APM documentation? It often has useful troubleshooting tips.

#### Customer:
I haven't checked that yet. Can you point me to the right section?

#### Java APM Agent:
Sure thing! Here's the link to New Relic's APM best practices documentation: Best Practices Documentation(https://docs.newrelic.com/)

#### Customer:
Thanks! 

#### Java APM Agent:
- Another important step you can take is running a CLI diagnostic to gather more detailed information about your setup. From the output of this command, you will receive a permalink. Copy that permalink to view the results of your latest Diagnostics CLI run. This will inform you about your environment's compatibility.

You can do this using the following link: [CLI Diagnostic Link](https://one.newrelic.com/nr1-core/help-xp/home?account=4540323&duration=604800000&state=eccc04e4-1ffd-d54b-6d2b-9618f5678c83)

- Additionally, please follow this link to common issues such as not seeing data
https://docs.newrelic.com/docs/new-relic-solutions/solve-common-issues/troubleshooting/not-seeing-data/

Make sure to select troubleshooting steps specific to the agent you are using (Java).

#### Customer:
Wow, thanks for the not seeing data link. Great, I will review and see what it turns up. Should I contact support if these steps don't resolve the issue?

#### Java APM Agent:
That's a good plan. However, let's go through some specific steps to ensure the New Relic Java agent is correctly configured:

Steps to Resolve:

- Download and Place New Relic Java Agent:

- Download the New Relic Java agent JAR file from the New Relic website.
Place the JAR file in a directory on your machine (e.g., C:\Program Files\NewRelic\newrelic.jar).
Update JVM Argument:

- Update your application's startup script or configuration to include the -javaagent argument pointing to the New Relic Java agent JAR file.
Check Java Version Compatibility:

- Verify the Java version running on your machine using java -version.
Compare it with the supported versions listed in the New Relic documentation.
If necessary, upgrade your Java version to ensure compatibility with the New Relic Java agent.

- Restart Your Application:

After making these changes, restart your Java application to apply the new configuration with the New Relic Java agent.

#### Customer:
Will do! Thanks for your help and guidance.

#### Java APM Agent:
You're welcome! Don't hesitate to reach out if you have any more questions or need further assistance. Good luck with the diagnostics and to ensure full data capture, please make sure to review database, trace insights, and transaction practices as outlined in the best practices.

#### Customer:
Thanks again, talk to you soon!

#### Java APM Agent:
Take care!


</BR>



# Phase II 

## New Relic Integration and Monitoring Guide

This guide provides step-by-step instructions for integrating New Relic with your Java application, monitoring its performance, and troubleshooting common issues. What I learned exploring te New Relic platform.

### Prerequisites

Before you begin, ensure you have the following:

- Java Development Kit (JDK) installed
- Maven build tool
- Integrated Development Environment (IDE) such as IntelliJ IDEA or Eclipse
- New Relic account (sign up at [New Relic](https://newrelic.com))
- New Relic Java agent downloaded ([Download Here](https://download.newrelic.com/newrelic/java-agent/newrelic-agent/current))


## Step 1: Sign up For New Relic

1. **Sign up for New Relic:** Go to [New Relic](https://newrelic.com) and sign up for an account if you haven't already.

2. **Download Java Agent:** Before downloading, ensure your environment is compatible.

3. **Configure Your Java Agent:** Run the following command after downloading:
Understood! Here's the complete guide formatted as a single block of Markdown text for easy copying:

```bash
java -javaagent:/path/to/newrelic-agent-8.13.0.jar -jar your-application.jar
```

### Set License Key

Set your New Relic license key:

```bash
export NEW_RELIC_LICENSE_KEY="117a45738417840377294c7c1649d41bFFFFNRAL"
```

### Start Application with Java Agent

Use the `-javaagent` JVM argument:

```bash
java -javaagent:/path/to/newrelic-agent-8.13.0.jar -jar your-application.jar
```

## Step 2: Verify Installation

After starting your application, verify the New Relic agent installation by checking the logs and New Relic dashboard.

### Useful Links

- [New Relic Dashboard](https://newrelic.com): Monitor your application's performance metrics, errors, and transactions.
- [New Relic Logs](https://newrelic.com/logs): View detailed logs from the New Relic agent.
- [New Relic Documentation](https://docs.newrelic.com): Comprehensive documentation for setup, configuration, and troubleshooting.

## OpenTelemetry and Distributed Tracing

OpenTelemetry is an open-source project that provides a set of APIs, libraries, agents, and instrumentation to collect distributed traces and metrics from applications. It aims to standardize and simplify observability across different languages and platforms.

#### What is Distributed Tracing?

Distributed Tracing is a method used to profile and monitor applications, especially those built using microservices architecture, where requests traverse multiple services. It tracks the lifecycle of a request as it travels through various components of an application. Key components of Distributed Tracing include:

- **Spans:** Represent individual units of work within a request. Each span has a start time, duration, and metadata such as service name, operation name, and tags.
  
- **Trace:** A collection of spans that represent a complete request path through the system. Traces provide end-to-end visibility into how requests flow across different services.

#### Key Benefits of OpenTelemetry and Distributed Tracing

- **End-to-End Visibility:** Gain insights into the complete journey of a request across services, helping to identify performance bottlenecks and latency issues.

- **Standardization:** OpenTelemetry provides a standardized way to instrument and collect telemetry data across various programming languages and frameworks, promoting consistency in observability practices.

- **Interoperability:** Integrates seamlessly with existing observability tools and platforms, allowing for better collaboration and sharing of telemetry data across teams.

- **Scalability:** Scales with modern, distributed architectures, enabling monitoring of applications regardless of size or complexity.

#### Getting Started with OpenTelemetry

To get started with OpenTelemetry, you typically need to:

1. **Instrument Your Application:** Integrate OpenTelemetry libraries or SDKs into your application code to capture trace data.

2. **Configure Exporters:** Define where and how the collected telemetry data (spans and metrics) should be exported. OpenTelemetry supports various exporters like Jaeger, Zipkin, Prometheus, and New Relic.

3. **Visualize and Analyze Data:** Use observability platforms or tools that support OpenTelemetry to visualize distributed traces and metrics, enabling deeper insights into application performance and behavior.

#### Learn More

Explore OpenTelemetry's documentation and community resources to delve deeper into instrumenting and leveraging distributed tracing for enhanced observability in your applications:

- [OpenTelemetry Documentation](https://opentelemetry.io/docs/)
- [GitHub Repository](https://github.com/open-telemetry/opentelemetry-specification)

OpenTelemetry and Distributed Tracing empower developers and operations teams to effectively monitor, troubleshoot, and optimize distributed systems, ensuring reliable and performant applications.


## Troubleshooting

During my installation process, I faced a few challenges, so here are a few common installation solutions.

#### Issue: New Relic Java Agent Jar Not Found

  **Error Message:** Failed to find the New Relic Java Agent Jar in the JVM argument.

  **Solution:** Ensure that you have downloaded the New Relic Java agent JAR file from the New Relic website. Place the JAR file in a directory on your machine. Update your application's startup script or configuration to include the `-javaagent` argument pointing to the New Relic Java agent JAR file.

#### Issue: Unsupported Java Vendor/Version Combination

  **Error Message:** Java processes running with unsupported vendor/version combinations.

  **Solution:** Check the Java version running on your machine against the supported versions listed in the New Relic documentation. Upgrade your Java version if necessary to ensure compatibility with the New Relic Java agent.

#### Issue: New Relic License Key Configuration

  **Error Message:** Application fails to connect to New Relic due to invalid or missing license key.

  **Solution:** Set your New Relic license key either in the New Relic configuration file (`newrelic.yml`) or as a system property (`NEW_RELIC_LICENSE_KEY`). Ensure that the key is correctly formatted and matches your New Relic account.

#### Issue: Connectivity and Firewall Settings

  **Error Message:** Application cannot connect to New Relic's servers.

  **Solution:** Verify your network settings and ensure that there are no firewall rules blocking outbound traffic to New Relic's endpoints (`collector.newrelic.com`, `metric-api.newrelic.com`, `insights-collector.newrelic.com`). Adjust firewall settings as necessary to allow communication.

#### Issue: Missing Application Data in New Relic

  **Error Message:** Data from your application is not appearing in the New Relic dashboard.

  **Solution:** Check the New Relic agent logs (`newrelic_agent.log`) for any errors or warnings related to data reporting. Ensure that your application is correctly instrumented with the New Relic Java agent and that there are no configuration issues preventing data transmission.

# Phase III

## Acknowledgments

Thank you to the following resources and individuals for their contributions and support:

- **New Relic Documentation:** Provided detailed information on APM setup, troubleshooting, and best practices.
- **OpenTelemetry Documentation:** Comprehensive guides on instrumenting applications and utilizing distributed tracing for observability.
- **Customer Support Session:** Valuable insights and feedback from customer interactions that helped refine troubleshooting strategies.

## References Used

- [New Relic Documentation](https://docs.newrelic.com/)
- [OpenTelemetry Documentation](https://opentelemetry.io/docs/)

These references were instrumental in understanding and implementing effective application monitoring and observability practices.
