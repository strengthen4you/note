# liangdabiao/claude-data-analysis: Create a data analysis AI agent with Claude Code. Make data analysis as simple as having a chat!​​ 别忘了！claude code也是agent框架，类似langgraph,crewAI，autogen等等agent框架。我改造claude code搞一个数据分析智能体AI。 让数据分析变得像聊天一样简单！
A modern, intelligent data analysis platform built with Claude Code's sub-agents, slash-commands, and hooks. Transform your data analysis workflow with AI-powered assistance.

Place your dataset in the `data_storage/` directory:

```shell
cp your_data.csv ./data_storage/
```

Use intuitive slash commands to analyze your data:

```shell
# Basic exploratory analysis
/analyze user_behavior_sample.csv exploratory

# Create visualizations
/visualize user_behavior_sample.csv all

# Generate analysis code
/generate python data-cleaning

# Create comprehensive report
/report user_behavior_sample.csv complete markdown
```

*   **data-explorer**: Expert statistical analysis and pattern discovery
*   **visualization-specialist**: Beautiful, insightful charts and graphs
*   **code-generator**: Production-ready analysis code
*   **report-writer**: Comprehensive analysis reports
*   **quality-assurance**: Data validation and quality control
*   **hypothesis-generator**: Research hypothesis and insights

*   `/analyze [dataset] [type]` - Perform data analysis
*   `/visualize [dataset] [type]` - Create visualizations
*   `/generate [language] [type]` - Generate analysis code
*   `/report [dataset] [format]` - Generate reports
*   `/quality [dataset] [action]` - Quality assurance
*   `/hypothesis [dataset] [domain]` - Generate hypotheses

*   **Data Validation**: Automatic quality checks on data upload
*   **Smart Context**: Project-aware analysis suggestions
*   **Reproducible Analysis**: Complete documentation and code generation

```shell
# Complete analysis workflow
/analyze user_behavior.csv exploratory
/visualize user_behavior.csv trends
/quality user_behavior.csv clean
/report user_behavior.csv complete html
/generate python user-segmentation
```

```shell
# Sales performance analysis
/analyze sales_data.csv statistical
/visualize sales_data.csv trends
/generate sql revenue-analysis
/report sales_data.csv executive pdf
```

```shell
# Customer segmentation
/analyze customer_data.csv predictive
/visualize customer_data.csv distribution
/generate r clustering-analysis
/hypothesis customer_data churn-prediction
```

```
claude-data-analysis/
├── .claude/
│   ├── agents/          # Sub-agent configurations
│   ├── commands/        # Slash command definitions
│   ├── hooks/          # Automation scripts
│   └── settings.json   # Claude Code settings
├── data_storage/       # Your data files
├── visualizations/     # Generated charts
├── generated_code/     # Analysis code
├── analysis_reports/   # Analysis reports
├── examples/          # Example datasets and workflows
└── docs/             # Documentation 
```

The project includes sample data to get you started:

*   **user\_behavior\_sample.csv**: Sample user behavior data with user actions, devices, locations, and revenue
*   **Field descriptions**: user\_id, session\_id, timestamp, action, page\_url, device\_type, location, revenue

The project uses Claude Code's configuration system. Key settings:

1.  **Hooks**: Automated validation and context loading
2.  **Sub-agents**: Specialized AI assistants for different tasks
3.  **Commands**: Custom slash commands for common operations

*   Python 3.8+ for data analysis
*   Claude Code with sub-agents enabled
*   Data files in CSV, JSON, or Excel format

1.  **Place your data** in `data_storage/`
2.  **Run exploratory analysis**: `/analyze your_data.csv exploratory`
3.  **Create visualizations**: `/visualize your_data.csv all`
4.  **Generate report**: `/report your_data.csv complete markdown`

1.  **Customize agents**: Modify `.claude/agents/` configurations
2.  **Create custom commands**: Add new commands in `.claude/commands/`
3.  **Set up automation**: Configure hooks in `.claude/settings.json`
4.  **Extend functionality**: Add custom analysis scripts

*   Data quality assessment
*   Summary statistics
*   Pattern discovery
*   Initial insights

*   Hypothesis testing
*   Correlation analysis
*   Regression analysis
*   Confidence intervals

*   Feature importance
*   Predictive modeling
*   Variable relationships
*   Model recommendations

*   All analysis types
*   Comprehensive reports
*   Visualizations
*   Actionable insights

*   Comprehensive dashboard
*   Multiple chart types
*   Interactive exploration
*   Executive summary

*   **Trends**: Time series, moving averages
*   **Distribution**: Histograms, box plots, density plots
*   **Correlation**: Heatmaps, scatter plots, correlation matrices
*   **Comparison**: Bar charts, grouped charts, small multiples

*   **Python**: Pandas, NumPy, Scikit-learn, Matplotlib
*   **R**: Tidyverse, ggplot2, caret
*   **SQL**: All major dialects
*   **JavaScript**: D3.js, Plotly.js, TensorFlow.js

*   Data cleaning and preprocessing
*   Statistical analysis
*   Machine learning
*   Visualization code
*   Custom analysis

**Current Phase**: Week 1.1 - Project Initialization ✅

*   Project structure and configuration
*   Data Explorer sub-agent
*   Visualization Specialist sub-agent
*   Core slash commands (/analyze, /visualize, /generate)
*   Automation hooks
*   Sample data and documentation

*   Report Writer sub-agent
*   Quality Assurance sub-agent
*   Hypothesis Generator sub-agent
*   Advanced slash commands
*   Interactive dashboards
*   Integration with external tools

We welcome contributions! Please follow these steps:

1.  **Fork the repository**
2.  **Create a feature branch**
3.  **Add your improvements**
4.  **Test your changes**
5.  **Submit a pull request**

*   Follow the established code style
*   Add comprehensive documentation
*   Include unit tests for new features
*   Update the README as needed

This project is licensed under the MIT License. See the LICENSE file for details.

*   Built with [Claude Code](https://claude.ai/code)
*   Inspired by the [DATAGEN](https://github.com/starpig1129/DATAGEN) project
*   Powered by modern data science tools and frameworks

For support and questions:

*   Check the documentation in the `docs/` directory
*   Review the examples in `examples/`
*   Use the `/help` command for usage assistance

* * *

**Start analyzing your data smarter, not harder!** 🚀