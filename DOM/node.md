1. Node原型链

   * div  HTMLDivElement =>HTMLElement=>Element=>Node=>EventTarget=>Object
   * div.attributes[0]  Attr=>Node=>EventTarget=>Object 
   * div.childNodes[0] Text=>CharacterData=>Node=>EventTarget=>Object

2. Node type

   | 常量                               | 值   | 描述                                                         |
   | :--------------------------------- | :--- | :----------------------------------------------------------- |
   | `Node.ELEMENT_NODE`                | `1`  | 一个 [`元素`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element) 节点，例如 [`<p>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/p) 和 [`<div>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/div)。 |
   | `Node.TEXT_NODE`                   | `3`  | [`Element`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element) 或者 [`Attr`](https://developer.mozilla.org/zh-CN/docs/Web/API/Attr) 中实际的  [`文字`](https://developer.mozilla.org/zh-CN/docs/Web/API/Text) |
   | `Node.PROCESSING_INSTRUCTION_NODE` | `7`  | 一个用于XML文档的 [`ProcessingInstruction`](https://developer.mozilla.org/zh-CN/docs/Web/API/ProcessingInstruction) ，例如 `<?xml-stylesheet ... ?>`声明。 |
   | `Node.COMMENT_NODE`                | `8`  | 一个 [`Comment`](https://developer.mozilla.org/zh-CN/docs/Web/API/Comment) 节点。 |
   | `Node.DOCUMENT_NODE`               | `9`  | 一个 [`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document) 节点。 |
   | `Node.DOCUMENT_TYPE_NODE`          | `10` | 描述文档类型的 [`DocumentType`](https://developer.mozilla.org/zh-CN/docs/Web/API/DocumentType) 节点。例如 `<!DOCTYPE html>`  就是用于 HTML5 的。 |
   | `Node.DOCUMENT_FRAGMENT_NODE`      | `11` | 一个 [`DocumentFragment`](https://developer.mozilla.org/zh-CN/docs/Web/API/DocumentFragment) 节点 |

   | 常量                         | 值   | 描述                                                         |
   | ---------------------------- | ---- | ------------------------------------------------------------ |
   | `Node.ATTRIBUTE_NODE`        | 2    | [`元素`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element) 的耦合[`属性`](https://developer.mozilla.org/zh-CN/docs/Web/API/Attr) 。在 [DOM4](https://www.w3.org/TR/dom/) 规范里[`Node`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node) 接口将不再实现这个元素属性。 |
   | `Node.CDATA_SECTION_NODE`    | `4`  | 一个 [`CDATASection`](https://developer.mozilla.org/zh-CN/docs/Web/API/CDATASection)。 在 [DOM4](https://www.w3.org/TR/dom/) 规范里被移除。 |
   | `Node.ENTITY_REFERENCE_NODE` | 5    | 一个 XML 实体引用节点。 在 [DOM4](https://www.w3.org/TR/dom/) 规范里被移除。 |
   | `Node.ENTITY_NODE`           | 6    | 一个 XML `<!ENTITY ...>`  节点。 在 [DOM4](https://www.w3.org/TR/dom/) 规范中被移除。 |
   | `Node.NOTATION_NODE`         | 12   | 一个 XML `<!NOTATION ...>` 节点。 在 [DOM4](https://www.w3.org/TR/dom/) 规范里被移除. |

3. 属性
   * [`Node.childNodes`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/childNodes)
   * [`Node.firstChild`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/firstChild) 
   * [`Node.isConnected`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/isConnected)
   * [`Node.lastChild`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/lastChild)
   * [`Node.nextSibling`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/nextSibling) 
   * [`Node.previousSibling`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/previousSibling)
   * [`Node.nodeName`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/nodeName) 
   * [`Node.nodeType`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/nodeType)
   * [`Node.nodeValue`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/nodeValue)
   * [`Node.ownerDocument`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/ownerDocument)
   * [`Node.parentNode`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/parentNode)
   * [`Node.parentElement`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/parentElement)
   * [`Node.textContent`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/textContent)
4. 方法
   * [`Node.appendChild()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/appendChild)
   * [`Node.cloneNode()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/cloneNode)
   * [`Node.compareDocumentPosition()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/compareDocumentPosition)
   * [`Node.contains()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/contains)
   * [`Node.getRootNode()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/getRootNode)
   * [`Node.hasChildNodes()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/hasChildNodes)
   * [`Node.insertBefore()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/insertBefore)
   * [`Node.isEqualNode()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/isEqualNode)
   * [`Node.normalize()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/normalize)
   * [`Node.removeChild()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/removeChild)
   * [`Node.replaceChild()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/replaceChild)

