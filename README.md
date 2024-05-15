# AutoCrawler

AUTOCRAWLER : A Progressive Understanding Web Agent for Web Crawler Generation
https://arxiv.org/abs/2404.12753 

AUTOCRAWLER can automatically generate code to extract information from webpages. Using LLM to understand the structure of a webpage and then write code to target the specific information that the user wants. Used to extract information from a variety of websites, even if the websites have different layouts 

Auto Crawler
- two-stage framework with progressive understanding to generate executable action sequences. 
- leverages the hierarchical structure of HTML for progressive understanding.

Tries to refine down to the specific node in the DOM tree containing the target information, and then moves up the DOM tree when execution fails

- LLMs are used for web automation capabilities like planning, reasoning, reflection, and tool use. 
- LLMs to construct generative agents that can autonomously navigate, interpret, and interact with web content

Existing web agent frameworks often demonstrate poor performance on open-world tasks and have insufficient reusability.

Working:
- Model the crawler generation task as an action sequence generation task. ie. generate an action sequence Aseq that consists of a sequence of XPath expression from a set of seed webpages
- Limiting the length and height of the DOM tree to improve the performance of LLM generation.
  - Performs traversal strategy consisting of top-down and step-back operations.
  - At each step, guiding the LLMs to directly write out the XPath leading to the node containing the target information and to judge whether the value extracted with XPath is consistent with the value it recognizes
  - If execution fails, then adopt a step-back operation to retreat from the failed node, ensuring the web page includes the target information, which is driven by LLMs

Datasets:
1. SWDE
1. EXTENDED SWDE
1. Ds1

- Design instructions for each of the domains, and for each of the attributes as the input information for LLMs
- For each website in each domain, sample 100 webpages as the whole test set
- Pre-process the websites by removing those elements in a webpage that do not contribute to the semantics
- Filter out all DOM element nodes with <script> and <style>, as well as delete all attributes in the element node except @class

Issues with LLMs in generating crawlers
- Pre-trained on massive corpora of cleansed, high-quality pure text, lacking exposure to markup languages such as HTML.
- Complexity of crawler generation because of semi-structured nature of HTML
- Inefficient in understanding the structural information of lengthy docs

Evaluation:
precision, recall, and F1 score.
IE task evaluation
Based on IE eval, categorize the executability of action sequences into the following six situations. 
1. Correct, both precision, recall and f1-score equal 1, which indicates the action sequence is precisely; 
1. Precision(Prec.), only precision equals 1, which indicates perfect accuracy in the instances extracted following the action sequence, but misses relevant instances; 
1. Recall(Reca.), only recall equals 1, which means that it successfully identifies all relevant instances in the webpage but incorrectly identifies some irrelevant instances;
1. Unexecutable(Unex.), recall equals 0, which indicates that the action sequence fails to identify relevant instances; 
1. Over-estimate(Over.), precision equals 0, which indicates that the action sequence extracts the instances while ground truth is empty; 
1. Else: the rest of the situation, including partially extracting the information, etc.

