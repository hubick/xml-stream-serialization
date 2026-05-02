# XML Stream Serialization

A Java library providing stream-based introspection/serialization/parsing of infinitely large objects using XML.

---


## Introspectable (`main` sub-module)

The provided `Introspectable` interface is implemented by an object to expose data/properties contained within itself.

An object implementing the `Introspectable` interface is required to define a single method, `introspect()`, returning an `Introspectable.Info` class.

An object implementing the `Introspectable` interface generally uses the nested `Info.Builder` class to create the `Info` object containing the data/properties it wishes to expose.

---


## XMLSerializable (`main` sub-module)

The provided `XMLSerializable` interface is implemented by an object to declare that it's capable of writing XML for itself to a `javax.xml.stream.XMLStreamWriter`.

An object implementing the `XMLSerializable` interface is required to define a single method, `writeXML()`, accepting an `XMLStreamWriter`, which performs this function.

The `Introspectable` interface extends `XMLSerializable`, *providing a default implementation*, so every `Introspectable` object is *automatically* `XMLSerializable`.

---


## Web Services (`ws-rs` sub-module)

The provided `MessageBodyWriter` classes allow you to define JAX-RS web services by simply implementing methods which return any `Introspectable`/`XMLSerializable` objects, which will then be *streamed* to clients as XML.

SOAP functionality is also provided via a `MessageBodyWriter` capable of writing out any `Introspectable`/`XMLSerializable` object within a SOAP `Envelope`, and an `ExceptionMapper` implementation which will return SOAP `Fault` XML for any exception thrown by your web service.

---


## XMLStreamParser (`parser` sub-module)

The provided `XMLStreamParser` class uses a `javax.xml.stream.XMLEventReader` to parse XML documents, binding their contents to a *stream* of target value objects which are dynamically constructed according to instructions you provide.

SOAP functionality is also provided via the `SOAPStreamParser` class, capable of parsing SOAP `Envelope`, `Header`, `Body`, and `Fault` elements.

---


## Documentation

Please see the sample code under `src/test/java/` within each sub-module, as well as the Javadoc on the provided classes for more detailed documentation.

