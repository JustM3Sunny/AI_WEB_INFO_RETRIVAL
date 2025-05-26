# 📚 WebInfo Retriever - Examples & Use Cases

This document provides comprehensive examples of how to use WebInfo Retriever for various scenarios.

## 🚀 **Quick Start Examples**

### **1. Ultra-Fast Comprehensive Search**

```bash
# Technology comparison
python -m webinfo_retriever.cli search --ultra-fast "React vs Vue.js performance comparison" --answer-type comparative

# Best practices research
python -m webinfo_retriever.cli search --ultra-fast "Python web scraping best practices" --num-results 8

# Tutorial discovery
python -m webinfo_retriever.cli search --ultra-fast "machine learning tutorials for beginners" --answer-type instructional
```

### **2. Comprehensive Research with File Output**

```bash
# Market research with detailed report
python -m webinfo_retriever.cli search --comprehensive "AI trends 2024" --output-file ai_trends_report.md --num-results 15

# Technical comparison study
python -m webinfo_retriever.cli search --comprehensive "Docker vs Kubernetes comparison" --answer-type comparative --output-file container_comparison.md

# Academic research
python -m webinfo_retriever.cli search --comprehensive "climate change impact studies" --num-results 20 --output-file climate_research.md
```

### **3. Fast Quick Answers**

```bash
# Quick factual answers
python -m webinfo_retriever.cli search --fast "What is GraphQL?"

# Simple comparisons
python -m webinfo_retriever.cli search --fast "Python vs JavaScript"

# Quick tutorials
python -m webinfo_retriever.cli search --fast "how to use Docker"
```

## 🐍 **Python API Examples**

### **1. Basic Usage**

```python
import asyncio
from webinfo_retriever import WebInfoRetriever

async def basic_example():
    client = WebInfoRetriever()
    
    # Ultra-fast comprehensive search
    result = await client.fast_comprehensive_search(
        query="What are the best Python web frameworks?",
        num_sources=8,
        answer_type="comparative"
    )
    
    print(result)  # Clean terminal output
    client.close()

asyncio.run(basic_example())
```

### **2. Advanced Research Example**

```python
import asyncio
from webinfo_retriever import WebInfoRetriever

async def research_example():
    client = WebInfoRetriever()
    
    # Comprehensive research with file output
    result = await client.comprehensive_search(
        query="Machine learning frameworks comparison 2024",
        num_sources=15,
        output_format="both",  # Terminal + file output
        answer_type="comparative"
    )
    
    # Display clean terminal output
    print(result["terminal_output"])
    
    # Save beautiful report
    with open("ml_frameworks_report.md", "w", encoding="utf-8") as f:
        f.write(result["markdown_report"])
    
    print("Report saved to ml_frameworks_report.md")
    client.close()

asyncio.run(research_example())
```

### **3. Batch Processing Example**

```python
import asyncio
from webinfo_retriever import WebInfoRetriever

async def batch_processing_example():
    client = WebInfoRetriever()
    
    queries = [
        "React best practices 2024",
        "Vue.js performance optimization",
        "Angular vs React comparison",
        "JavaScript frameworks trends"
    ]
    
    results = []
    for query in queries:
        print(f"Processing: {query}")
        result = await client.fast_comprehensive_search(
            query=query,
            num_sources=6,
            answer_type="comprehensive"
        )
        results.append({"query": query, "result": result})
    
    # Process results
    for item in results:
        print(f"\n{'='*60}")
        print(f"Query: {item['query']}")
        print(f"{'='*60}")
        print(item['result'][:500] + "...")  # First 500 chars
    
    client.close()

asyncio.run(batch_processing_example())
```

### **4. Single URL Analysis Example**

```python
from webinfo_retriever import WebInfoRetriever

def url_analysis_example():
    client = WebInfoRetriever()
    
    # Analyze a specific webpage
    result = client.retrieve_and_summarize(
        url="https://realpython.com/python-web-scraping/",
        query="What are the main web scraping techniques covered?"
    )
    
    print("Summary:", result['summary'])
    print("Key Points:", result.get('key_points', []))
    print("Metadata:", result.get('metadata', {}))
    
    client.close()

url_analysis_example()
```

## 🎯 **Use Case Examples**

### **1. Academic Research**

```python
import asyncio
from webinfo_retriever import WebInfoRetriever

async def academic_research():
    client = WebInfoRetriever()
    
    # Research topic with multiple perspectives
    result = await client.comprehensive_search(
        query="renewable energy efficiency studies 2024",
        num_sources=20,
        output_format="both",
        answer_type="comprehensive"
    )
    
    # Save detailed academic report
    with open("renewable_energy_research.md", "w", encoding="utf-8") as f:
        f.write(result["markdown_report"])
    
    # Get citations for academic use
    citations = client.answer_formatter.create_citation_list(
        result["answer_object"]
    )
    
    with open("citations.md", "w", encoding="utf-8") as f:
        f.write(citations)
    
    print("Academic research completed!")
    print("Report saved to: renewable_energy_research.md")
    print("Citations saved to: citations.md")
    
    client.close()

asyncio.run(academic_research())
```

### **2. Market Research**

```python
import asyncio
from webinfo_retriever import WebInfoRetriever

async def market_research():
    client = WebInfoRetriever()
    
    # Analyze market trends
    result = await client.fast_comprehensive_search(
        query="AI startup trends and investment 2024",
        num_sources=12,
        answer_type="comprehensive"
    )
    
    # Quick summary for executives
    summary = client.answer_formatter.create_quick_summary(
        result if hasattr(result, 'query') else None
    )
    
    print("Executive Summary:")
    print(summary)
    
    client.close()

asyncio.run(market_research())
```

### **3. Technology Comparison**

```python
import asyncio
from webinfo_retriever import WebInfoRetriever

async def tech_comparison():
    client = WebInfoRetriever()
    
    # Compare technologies
    result = await client.fast_comprehensive_search(
        query="PostgreSQL vs MongoDB performance comparison",
        num_sources=10,
        answer_type="comparative"
    )
    
    print(result)
    
    # Get detailed comparison
    detailed_result = await client.comprehensive_search(
        query="PostgreSQL vs MongoDB detailed comparison use cases",
        num_sources=15,
        output_format="both",
        answer_type="comparative"
    )
    
    # Save comparison report
    with open("database_comparison.md", "w", encoding="utf-8") as f:
        f.write(detailed_result["markdown_report"])
    
    print("Detailed comparison saved to: database_comparison.md")
    
    client.close()

asyncio.run(tech_comparison())
```

### **4. Content Creation Research**

```python
import asyncio
from webinfo_retriever import WebInfoRetriever

async def content_research():
    client = WebInfoRetriever()
    
    # Research for blog post
    topics = [
        "Python async programming best practices",
        "FastAPI vs Flask performance",
        "Python testing frameworks comparison"
    ]
    
    blog_research = {}
    
    for topic in topics:
        print(f"Researching: {topic}")
        
        result = await client.fast_comprehensive_search(
            query=topic,
            num_sources=8,
            answer_type="comprehensive"
        )
        
        blog_research[topic] = result
    
    # Create content outline
    outline = "# Blog Post Research\n\n"
    for topic, research in blog_research.items():
        outline += f"## {topic}\n\n"
        outline += f"Research Summary: {research[:300]}...\n\n"
    
    with open("blog_research_outline.md", "w", encoding="utf-8") as f:
        f.write(outline)
    
    print("Content research completed!")
    print("Outline saved to: blog_research_outline.md")
    
    client.close()

asyncio.run(content_research())
```

## 🔧 **Advanced Configuration Examples**

### **1. Custom Configuration**

```python
from webinfo_retriever import WebInfoRetriever
from webinfo_retriever.utils.config import Config

# Custom configuration
config = Config()
config.set("scraping.timeout", 15)
config.set("ai.model", "gemini-2.0-flash-exp")
config.set("search.max_results", 25)
config.set("ai.temperature", 0.3)

client = WebInfoRetriever(config=config)
```

### **2. Environment-Based Configuration**

```bash
# Set environment variables
export GEMINI_API_KEY="your_api_key"
export WEBINFO_TIMEOUT="20"
export WEBINFO_MAX_RETRIES="5"
export WEBINFO_CACHE_ENABLED="true"
export WEBINFO_LOG_LEVEL="INFO"
```

```python
from webinfo_retriever import WebInfoRetriever

# Configuration from environment
client = WebInfoRetriever()  # Automatically uses env vars
```

### **3. Performance Optimization**

```python
import asyncio
from webinfo_retriever import WebInfoRetriever

async def optimized_search():
    client = WebInfoRetriever()
    
    # Optimized for speed
    result = await client.fast_comprehensive_search(
        query="Python performance optimization techniques",
        num_sources=15,  # More sources for better coverage
        answer_type="comprehensive",
        stream_results=True  # Enable streaming for faster feedback
    )
    
    print(result)
    client.close()

asyncio.run(optimized_search())
```

## 📊 **Output Format Examples**

### **1. Terminal Output**
```
🔍 COMPREHENSIVE SEARCH ANALYSIS
============================================================

🎯 QUERY: "Python web frameworks comparison"

📋 DIRECT ANSWER:
--------------------
Django and Flask are the most popular Python web frameworks...

📊 SUMMARY METRICS:
• Confidence Level: Good (74.8%)
• Answer Type: Comparative
• Processing Time: 18.32s
• Sources Analyzed: 8

💡 KEY INSIGHTS & DISCOVERIES:
-----------------------------------
1. Django excels in rapid development and security
2. Flask prioritizes flexibility and developer choice
3. FastAPI is gaining popularity for API development
...
```

### **2. File Output (Markdown with HTML styling)**
```html
# 🔍 **COMPREHENSIVE SEARCH ANALYSIS**

<div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 20px; border-radius: 10px; color: white; margin: 20px 0;">

## 🎯 **Query:** "Python web frameworks comparison"

</div>

---

## 📋 **DIRECT ANSWER**

<div style="background: #f8f9fa; border-left: 5px solid #28a745; padding: 15px; margin: 15px 0; border-radius: 5px;">

### Django and Flask are the most popular Python web frameworks...

</div>
```

### **3. JSON Output**
```json
{
  "query": "Python web frameworks comparison",
  "direct_answer": "Django and Flask are the most popular...",
  "confidence_score": 0.748,
  "processing_time": 18.32,
  "sources": [
    {
      "title": "Django Documentation",
      "url": "https://docs.djangoproject.com/",
      "quality_score": 0.95,
      "summary": "Django is a high-level Python web framework..."
    }
  ]
}
```

## 🎯 **Best Practices**

### **1. Query Optimization**
```python
# Good queries
"React vs Vue.js performance comparison"  # Specific comparison
"Python machine learning libraries 2024"  # Time-specific
"Docker best practices for production"     # Specific use case

# Less optimal queries
"programming"                              # Too broad
"help me"                                 # Not specific
"what is good"                            # Vague
```

### **2. Source Management**
```python
# For quick answers
num_sources=5-8

# For comprehensive research
num_sources=12-20

# For academic research
num_sources=15-25
```

### **3. Answer Type Selection**
```python
# Use appropriate answer types
answer_type="comparative"     # For A vs B queries
answer_type="instructional"   # For how-to queries
answer_type="factual"        # For what/when/where queries
answer_type="comprehensive"  # For general research
```

---

**For more examples and advanced usage, visit our [GitHub repository](https://github.com/JustM3Sunny/webinfo-retriever) or check the [documentation](https://github.com/JustM3Sunny/webinfo-retriever/wiki).**
