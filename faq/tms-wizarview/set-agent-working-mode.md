# Set Agent Working Mode

1. Access Terminal or Group Settings:
   * In the TMS interface, navigate to 'Terminals > Terminal/Group'.
2. Open System Parameter Configuration:
   * Click on the 'Configure System Parameter' icon. This action will open the System Parameter page.
3. Select the System Mode:
   * On the System Parameter page, click on 'System'.
   * Here, you can set the Agent Working Mode. There are four modes to choose from, 'Default' is also 'Full Function'.

| Mode              | Description                                                                                                                                                         | Data Usage                                               |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| Full Function     | Enables all functions of the Agent.                                                                                                                                 | Approximately 5-10 MB per month, varying based on usage. |
| Standard          | Major functions of the Agent are enabled.                                                                                                                           | Around 3-5 MB per month.                                 |
| Low Traffic       | Maintains the terminal online with minimal activity (heart beating). The terminal will not actively request the TMS server except for the first time after booting. | About 1-2 MB per month.                                  |
| Ultra-low Traffic | Keeps the terminal online with very low frequency heartbeats, potentially causing delayed responses to TMS commands.                                                | Less than 300 KB per month.                              |

Note:

* Choose the mode based on your data usage preferences and operational needs. Each mode balances functionality with data consumption, allowing you to optimize based on the specific requirements of your terminal network.
