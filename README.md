# Smart CPG Decision Support Agent

An intelligent decision support system leveraging GenAI and Agentic AI to automate CPG business analytics and strategy formulation.

## 🎯 Features

- **Multi-Store, Multi-SKU Data Ingestion:** Process large-scale sales data in Azure Databricks
- **Automated Trend Analysis:** Extract sales trends, seasonality, and patterns
- **Anomaly Detection:** Identify revenue spikes, inventory risks, and demand changes
- **Scenario Simulation:** Test promotions, price changes, and supply shortages
- **Agentic AI Loop:** Intelligent tool orchestration with LangChain
- **Natural Language Interface:** Ask questions and get strategy memos in plain English
- **Interactive UI:** Streamlit dashboard for business users

## 📁 Project Structure

```
smart-cpg-decision-agent/
├── data/                    # Data files
├── notebooks/               # Databricks notebooks for prototyping
├── scripts/
│   └── generate_data.py     # Synthetic data generator
├── src/
│   ├── data_loader.py       # Data ingestion module
│   ├── tools/
│   │   ├── trend_analysis.py       # Trend analyzer tool
│   │   ├── anomaly_detection.py    # Anomaly detector tool
│   │   └── scenario_simulation.py  # Scenario simulator tool
│   ├── genai/
│   │   └── llm_interface.py        # Azure OpenAI interface
│   ├── agent/
│   │   ├── agent_core.py           # Main agent orchestrator
│   │   └── memory.py               # Conversation memory
│   └── ui/
│       └── streamlit_app.py        # Streamlit UI
├── tests/                   # Unit tests
├── requirements.txt         # Python dependencies
├── .env.example            # Environment variables template
└── README.md               # This file
```

## 🚀 Quick Start

### 1. Clone and Setup

```bash
# Clone repository
cd smart-cpg-decision-agent

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Configure Environment

```bash
# Copy environment template
cp .env.example .env

# Edit .env with your Azure OpenAI credentials
# AZURE_OPENAI_KEY=your_key_here
# AZURE_OPENAI_ENDPOINT=https://your-resource.openai.azure.com/
```

### 3. Generate Sample Data

```bash
cd scripts
python generate_data.py
```

This creates:
- `data/cpg_sales_sample_50000.csv`
- `data/cpg_sales_data.parquet`

### 4. Run Streamlit UI

```bash
streamlit run src/ui/streamlit_app.py
```

Then open http://localhost:8501 in your browser.

## 💻 Usage Examples

### Conversational Queries

```python
from src.data_loader import CPGDataLoader
from src.agent.agent_core import CPGDecisionAgent
import pandas as pd

# Load data
data = pd.read_parquet('data/cpg_sales_data.parquet')

# Initialize agent
agent = CPGDecisionAgent(
    data=data,
    azure_openai_key="your_key",
    azure_openai_endpoint="your_endpoint"
)

# Ask questions
result = agent.query("What are the top performing product categories?")
print(result['answer'])

# Simulate scenarios
result = agent.query("Simulate a 25% discount promotion on beverages")
print(result['answer'])

# Generate comprehensive report
report = agent.generate_comprehensive_report()
print(report)
```

### Direct Tool Usage

```python
from src.tools.trend_analysis import TrendAnalyzer
from src.tools.scenario_simulation import ScenarioSimulator

# Trend analysis
analyzer = TrendAnalyzer()
trend = analyzer.analyze_overall_trend(data)
print(trend['interpretation'])

# Scenario simulation
simulator = ScenarioSimulator()
promo_result = simulator.simulate_promo_campaign(
    data, 
    promo_discount=0.2,
    expected_volume_lift=1.5
)
print(promo_result['recommendation'])
```

## 🏗️ Architecture

The system follows a five-layer architecture:

1. **Data Layer:** PySpark/Pandas data loading and preprocessing
2. **Tool Layer:** Specialized analysis tools (trends, anomalies, simulations)
3. **GenAI Layer:** Azure OpenAI for natural language generation
4. **Agent Layer:** LangChain-based autonomous agent orchestrating tools
5. **UI Layer:** Streamlit interface for business users

## 🧪 Testing

```bash
# Run all tests
pytest tests/

# Run with coverage
pytest --cov=src tests/
```

## 🔧 Azure Databricks Deployment

### Upload to Databricks

1. Upload project to Databricks Repos
2. Install dependencies via cluster UI or notebook:

```python
%pip install -r requirements.txt
```

### Use in Notebook

```python
from src.data_loader import CPGDataLoader
from src.agent.agent_core import CPGDecisionAgent

# Load data
loader = CPGDataLoader(spark)
data = loader.load_parquet("dbfs:/FileStore/cpg_sales_data.parquet")

# Initialize agent
agent = CPGDecisionAgent(
    data=data.toPandas(),
    azure_openai_key=dbutils.secrets.get("openai", "api-key"),
    azure_openai_endpoint=dbutils.secrets.get("openai", "endpoint")
)

# Query
result = agent.query("Analyze Q4 performance")
print(result['answer'])
```

## 🔐 Security Best Practices

- Store Azure OpenAI credentials in Databricks Secrets
- Never commit `.env` file to version control
- Use environment variables for sensitive configuration
- Implement RBAC for production deployments

## 📊 Key Technologies

- **Data Processing:** PySpark, Pandas, NumPy
- **Machine Learning:** Scikit-learn, Scipy, Statsmodels
- **GenAI:** Azure OpenAI GPT-4
- **Agentic AI:** LangChain
- **UI:** Streamlit
- **Platform:** Azure Databricks

## 📝 Example Questions for Agent

- "What are the overall sales trends?"
- "Which product categories are performing best?"
- "Are there any unusual patterns or anomalies?"
- "Which stores are underperforming?"
- "How effective are our promotional campaigns?"
- "What would happen if we increase prices by 10%?"
- "Simulate a 20% discount promotion across all stores"
- "Identify inventory risks and stockout threats"

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

MIT License - see LICENSE file for details

## 🙏 Acknowledgments

- Built for CPG business intelligence and decision support
- Powered by Azure OpenAI and LangChain
- Designed for Azure Databricks deployment

## 📞 Support

For questions or issues:
- Open an issue on GitHub
- Contact: [Your contact information]

---

**Built with ❤️ for CPG Decision Makers**
