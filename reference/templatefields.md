---
title: Feldtypen für die Templates
---

# Feldtypen für die Templates

| Feldname | Typ für das Template |
|----------+----------------------|
| CompletedDate | element |
| CompletedYear | element |
| ContributingCorporation | element |
| CreatingCorporation | element |
Edition | element |
IdentifierIsbn | element |
IdentifierIssn | element |
IdentifierOpac | element |
IdentifierOpus3 | element |
IdentifierUrn | element |
Institute  | element oder group |
Issue | element |
Language | element |
Licence | element |
Note | element |
PageFirst | element |
PageLast | element |
PageNumber | element |
PersonAdvisor | group |
PersonAuthor | group |
PersonContributor | group |
PersonEditor | group |
PersonReferee | group |
PersonSubmitter | group |
PersonTranslator | group |
PublicationState | element |
PublishedDate | element |
PublishedYear | element |
PublisherName | element |
PublisherPlace | element |
SubjectSwd | element oder group |
SubjectUncontrolled | element oder group |
SubjectCCS | element oder group |
SubjectDDC | element oder group |
SubjectMSC | element oder group |
SubjectPACS | element oder group |
ThesisDateAccepted | element |
ThesisGrantor | element |
ThesisPublisher | element |
TitleAbstract | group |
TitleAdditional | group |
TitleMain | group |
TitleParent | group |
TitleSub | group |
Volume | element |

## Felder die als Group oder Element verwendet werden können

Bei den Felder, die Element oder Group sein können hängt dies von der gewünschten Multiplicity ab, ob für das Feld nur
ein oder mehrere Werte eingegeben werden können.

Für beliebig viele Werte (Group):

{% highlight phml %}
<?= $this->group($this->groupSubjectSwd); ?>
{% endhighlight %}

Für eine Beschränkung auf einen Wert (Element):

{% highlight phtml %}
<?= $this->element($this->SubjectSwd); ?>
{% endhighlight %}


